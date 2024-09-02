---
layout: post

title: How To Jekyll
imgUrl: /assets/img/posts/2024/jekyll-the-jackal.jpg

imgCaption: The Jekyll Jackel? | Photo by Benjamin Farren 
imgCaptionSrc: https://www.pexels.com/photo/jackal-in-grassland-15705591/

date: 2024-08-28 1:47:04 -0400
categories: blog
---
## Intro

Apart from the occasional GitHub-er or fanboy, I feel that not many people talk about Jekyll anymore. It can be useful for setting up a simple static website as fast as possible.

If you need a more complex application, especially one that is not static, Jekyll may not be the best option. That said, you will need some HTML, CSS, and possibly JavaScript depending on what you are trying to achieve.

If you are still reading, here is a quick surface-level overview of Jekyll, The Good, The Bad, And the Ruby.

## Getting Started

To get started, install Ruby, bundler, and Jekyll itself.

The Ruby dev environment can be installed on Windows or Linux. Granted I have had odd experiences with Windows in the past. So if you can, maybe lean towards Linux.

### Linux Install

```
sudo apt install ruby-full
sudo apt install jekyll
```

### Windows Install

For Windows, I highly recommend using the “Jekyll on Windows” Instructions: https://jekyllrb.com/docs/installation/windows/. But here are the general steps anyway. Keep in mind you can install Windows  Subsystem for Linux (WSL) so that installing Jekyll is not as annoying, but if you don’t like Linux or want to deal with it then don’t.

Run the Ruby Installer: https://rubyinstaller.org/

Then install Jekyll using gem

```
gem install jekyll bundler
```

### Create A Project

Note that you may need to run these commands as an admin or root. So don’t forget to preface with ‘sudo’ on linux if needed.

```
bundle exec jekyll new project-name
```
OR
```
mkdir project-name
cd project-name
bundle exec jekyll new .
```

The general layout of a Jekyll website looks like this. The bundle command should automatically generate most it.

```
_includes/
_layouts/
_posts/
assets/
_config.yml
index.md
```

## Initial Preparation

Once the project is generated, its probably a good idea to take a look at the Gemfile. The Gemfile is where we define resources and dependencies needed for the project. Usually Jekyll will try to be “helpful” and add stuff we don’t need for a base project.

(If you do like the default junk, then move on to the next section)

Open up the Gemfile and remove anything related to a theme like ‘minima’ etc. If you know what you are doing, then remove anything else you don’t want.

Then read the comments, they can be rather helpful.

```
source "https://rubygems.org"
# Hello! This is where you manage which Jekyll version is used to run.
# When you want to use a different version, change it below, save the
# file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
#
#     bundle exec jekyll serve
#
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!
gem "jekyll", "~> 4.3.1"
# This is the default theme for new Jekyll sites. You may change this to anything you like.
gem "minima", "~> 2.5"
# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.
# gem "github-pages", group: :jekyll_plugins
# If you have any plugins, put them here!
group :jekyll_plugins do
 gem "jekyll-feed", "~> 0.12"
end

# Windows and JRuby does not include zoneinfo files, so bundle the tzinfo-data gem
# and associated library.
platforms :mingw, :x64_mingw, :mswin, :jruby do
 gem "tzinfo", ">= 1", "< 3"
 gem "tzinfo-data"
end

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]

# Lock `http_parser.rb` gem to `v0.6.x` on JRuby builds since newer versions of the gem
# do not have a Java counterpart.
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
```

## Running The App

In the root of the project, add your page md files for your pages. The index.md or index.markdown will typically be the home page.

Then start the application.

```
bundle exec jekyll serve
```

You should be able to reach these pages from the browser. The default port is usually 4000. Make sure to add something the the index.mardown or index.md file or the page will probably be blank by default.

Home Page:
```
http://localhost:4000/
```

If you get an error like this: 

“... check_for_activated_spec!': You have already activated public_suffix 6.0.1, but your Gemfile requires public_suffix 4.0.6. …”

Or its complaining about not finding a specific dependency Then try to clean out the bundle.

```
bundle clean --force
```
Then run the bundle exec command again.

## Includes and Layouts

What makes Jekyll useful for customization, and also a menace if abused are the _includes and _layouts directories.

You can think of “layouts” as extendable/reusable page structures and “includes” as chunks or blocks of reusable pages.

Each markdown page can optionally extend a layout in the _layouts directory. Then typically you can ‘include’ a block of HTML in a layout or markdown file.

This allows for some code reuse and segmentation of purpose. If that sounds confusing, here is an extremely simple example. This is where knowing some CSS and HTML will help.

## Plugins

Jekyll allows for some ready-to-use out-of-the-box plugging for SEO and page structure.

For example, the jekyll-seo-tag plugin will dynamically populate most if not all needed meta tags for basic SEO needs and social cards.

## Why

Manipulating pages with weird braces is great and all, but why would you use Jekyll over any other framework? It comes down to preference, but my argument is simplicity if you need a simple and customizable static website. 

Emphasis on simple. If you try to make your app 'fancy', Jekyll's charm becomes its biggest flaw. The structure can become bulky and confusing to debug, especially if you don't have any experience with web development.
