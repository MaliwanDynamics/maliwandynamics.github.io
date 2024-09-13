---
layout: post

title: Jekyll Syntax Highlighting
imgUrl: /assets/img/post/sept-2024/syntax-highlight-computer-head-img.jpg

imgCaption: Glowing Syntax
imgCaptionSrc: https://www.pexels.com/photo/blue-and-red-light-from-computer-1933900/

date: 2024-08-14 12:00:00 -0400
categories:
- blog
- software
---
So you spun up a Jekyll website and you need to add a code snippet to a new post. But wait! It's ugly as h*ll! Why? How do other websites get their code to look so pretty and shiny?

Well, as with any website, not just Jekyll, there are several options. If you are on Github pages, then I recommend using the default [Rouge](https://github.com/rouge-ruby/rouge) configuration. If you are already using [Karmdown](https://kramdown.gettalong.org/), then you can opt to use [Github Flavored Markdown (GFM)](https://github.github.com/gfm/) and set Rogue as your syntax highlighter.

I personaly had issues with Kramdown in conjunction with every other parser other than Rogue on Github Pages, which is why I am reccomending Rouge as-is out of the box.

If that is not to your fancy, [Kramdown and Coderay](https://github.com/kramdown/syntax-coderay) together is another popular solution.

I also highly recommend reading the documentation if you feel lost, but if you are lazy and want the answer fast, here you go.

## The Plain Rouge Option

### Install Rouge

With Jekyll installed there is a high probability you also have the rouge gem installed. If not, you can install it and add it to the Gemfile as needed.

```ruby
gem ‘rouge’
```

### Add CSS For Rouge

If you have ever tried to set up syntax highlighting in Jekyll before you may have heard of [Pygments](https://pygments.org/). If not, just know you need some additional CSS that will hydrate the classes that Rouge adds to the HTML for code blocks.

This is where I got my CSS from: [Pygments CSS Themes](https://jwarby.github.io/jekyll-pygments-themes/languages/ruby.html)

Once obtained, add it to a CSS file in your project and import it. I went the SCSS route, so I was able to import it into the main body of CSS.

```css
@import my-css-theme
```

## Customize Rouge

### 1. Override The `.highlight` CSS Class

Rouge will add a .highlight CSS class to the generated HTML of the code blocks. Override it to add flavor to the blocks.

```css
.highlight {
    background-color: lightblue;
    padding: 1rem;
    border-radius: 10px;

    overflow-x: scroll;
}
```

### 2. Rouge Configuration

- [Rouge Github](https://github.com/rouge-ruby/rouge)
- [Rouge Jekyll Docs](https://jekyllrb.com/docs/liquid/tags/#code-snippet-highlighting)


---
## The Kramdown Option

### If Using Rogue

```ruby
gem 'kramdown', '~> 2.3'
```

### If Using Coderay

```ruby
gem 'kramdown', '~> 2.3'
gem "kramdown-syntax-coderay"
```

### Bundle Install Gems

Double-check this is the version of Kramdown you want. Then Make sure to stop the Jekyll server if it is already running and run a bundle install.

```shell
bundle install
```

You should be able install these with gem, but it gave me flack about missing dependencies. So I had to run a `bundle clean --force`, then bundle install instead to get around it.

I'm running Linux for this example, but you should get a similar result if you are on Windows.

```shell
Bundle complete! 7 Gemfile dependencies, 31 gems now installed.
Use `bundle info [gemname]` to see where a bundled gem is installed.
```

### Update the Configuration

Now run over to the _config.yml file in the root of your project and add some YAML.

#### Yaml For Kramdown + Rouge

```yaml
markdown: kramdown
kramdown:
  input: GFM
  syntax_highlighter: rouge
```

#### Yaml For Kramdown + Coderay

```yaml
markdown: kramdown
kramdown:
  syntax_highlighter: coderay
  coderay_line_numbers: ''
```

Keep in mind this is a minimal configuration, there are tons of other configuration options. I took the liberty of disabling line numbers for coderaty because it looks gross by default, but feel free to remove that.

## Customize Kramdown and Coderay

### 1. Override The `.code` CSS Class

Coderay will add a .code CSS class to the generated HTML of the code blocks. Override it to add flavor to the blocks.

```css
.code {
    background-color: lightblue;
    padding: 1rem;
    border-radius: 10px;

    overflow-x: scroll;
}
```

### 2. Kramdown and Coderay Configuration

- [Kramdown Coderay Github](https://github.com/kramdown/syntax-coderay)
- [Kramdown Coderay Jekyll Docs](https://jekyllrb.com/docs/configuration/markdown/)

---

## Tips And Issues

### Raw Liquid

If you are trying to add a code snippet with some Jekyll Liquid code, chances are the code between the braces will be executed. Even inside the the code element!

In this case you can put a `raw` block around the snippet to ensure Jekyll does not exeucte it. For example.

{% include /components/general-figure.html figureImg='/assets/img/post/sept-2024/jekyll-raw-tag.png' %}

### Markdown Code Fences

If you are trying to use the 3 tildies to block out a snippet, the highlighter you are using may not support it out of the box. You man need to use some Liquid to initiate it like so.

{% include /components/general-figure.html figureImg='/assets/img/post/sept-2024/jekyll-highlight-tag.png' %}
