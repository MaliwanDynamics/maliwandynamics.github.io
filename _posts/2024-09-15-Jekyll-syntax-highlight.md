---
layout: post

title: Jekyll Syntax Highlighting
imgUrl: /assets/img/post/sept-2024/syntax-highlight-computer-head-img.jpg

imgCaption: Glowing Syntax
imgCaptionSrc: https://www.pexels.com/photo/blue-and-red-light-from-computer-1933900/

date: 2024-09-15 12:00:00 -0400
categories:
- blog
- software
---
So you spun up a Jekyll website, and you need to add a code snippet to your new post.

But wait! It's ugly as all f***k! Why? How do other websites get their code to look so pretty and shiny?

Well [Kramdown and Coderay](https://github.com/kramdown/syntax-coderay) together is one popular solution. I recommend reading the documentation first, but if you are lazy and want the answer fast, here you go.

## Add The Gems

Go to your Gemfile in the root of your project and add Kramdown and Coderay gemmies.

Yes… gemmies.

```ruby
gem 'kramdown', '~> 2.3'
gem "kramdown-syntax-coderay"
```

Double-check this is the version of Kramdown you want. Then Make sure to stop the Jekyll server if it is already running.

Run a bundler install.

```shell
bundle install
```

I'm running Debian Linux for this example, but you should get a similar result.

```shell
Installing kramdown-syntax-coderay 1.0.1
Bundle complete! 7 Gemfile dependencies, 31 gems now installed.
Use `bundle info [gemname]` to see where a bundled gem is installed.
```

## Update the Configuration

Now run over the the _config.yml file which is also in the root of the project to add some fluff. Keep in mind this is a minimal configuration, there are lots of other configuration options.

```yaml
markdown: kramdown
kramdown:
  syntax_highlighter: coderay
  coderay_line_numbers: ''
```

I took the liberty of disabling line numbers because it looks gross, but feel free to remove that.

## Initiate Syntax Highlighting

To initiate the syntax highlight, add the language name right of the 3 tildies like so.

```
```html
```

So after a server reboot, you should now have syntax highlighting.

## Customize

If you feel the syntax is still a bit ugly, you have a few options.

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

[Kramdown and Coderay](https://github.com/kramdown/syntax-coderay) give several options for additional customization.