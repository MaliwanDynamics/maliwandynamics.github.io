---
layout: post

title: Syntax Highlighting For Code Snippets In Jekyll
imgUrl: /assets/img/post/sept-2024/syntax-highlight-computer-head-img.jpg

imgCaption: Glowing Syntax
imgCaptionSrc: https://www.pexels.com/photo/blue-and-red-light-from-computer-1933900/

date: 2024-09-14 12:00:00 -0400
categories:
- blog
- software
---
So I spun up a [Jekyll](https://jekyllrb.com/docs/) website and I needed to add code snippets to a new post. But wait! It's ugly as h*ll! Why? How do other websites get their code to look so pretty and shiny?

If you have no clue what I am talking about, check out the [Markdown Guide](https://www.markdownguide.org/extended-syntax/#fenced-code-blocks) on it.

If you are on [GitHub Pages](https://pages.github.com/), then I recommend using the default [Rouge](https://github.com/rouge-ruby/rouge) configuration. If you are already using [Karmdown](https://kramdown.gettalong.org/), then you can opt to use [GitHub Flavored Markdown (GFM)](https://github.github.com/gfm/) and set Rogue as your syntax highlighter.

I had issues on GitHub Pages with Kramdown in conjunction with every other parser other than Rogue, which is why I am recommending Rouge as-is instead.

If that is not to your fancy, or you are not on GitHub Pages, [Kramdown and Coderay](https://github.com/kramdown/syntax-coderay) together is another popular solution.

Also, try reading the documentation first if you feel lost, but if you are lazy and want the answer fast, here you go.

## The Plain Rouge Option

### Install Rouge

With Jekyll installed there is a high probability you also have the Rouge gem installed. If not, you can install it and add it to the Gemfile as needed.

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

Rouge will add a .highlight CSS class to the generated HTML of the code blocks. Override it to add additional flavor to the blocks.

```css
.highlight {
  padding: .3rem;
}

.highlighter-rouge {
  background-color: $master-accent;
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

Double-check this is the version of Kramdown you want. Then make sure to stop the Jekyll server if it is already running and run a bundle install.

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

Keep in mind this is a minimal configuration, there are tons of other configuration options. I took the liberty of disabling line numbers for Coderaty because it looks gross by default, but feel free to remove that.

## Customize Kramdown and Coderay

### 1. Override The `.code` CSS Class

Coderay will add a .code CSS class to the generated HTML of the code blocks. Override it to add additional flavor to the blocks.

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

If you are trying to add a code snippet with some Jekyll Liquid/Ruby code, chances are the code between the braces will be executed. Even inside the code element!

In this case you can put a `raw` block around the snippet to ensure Jekyll does not execute it. For example,

{% include /components/general-figure.html figureImg='/assets/img/post/sept-2024/jekyll-raw-tag.png' %}

### Markdown Code Fences

If you are trying to use the 3 tildies to block out a snippet, the highlighter you are using may not support it out of the box. You may need to use some code to initiate it like so.

{% include /components/general-figure.html figureImg='/assets/img/post/sept-2024/jekyll-highlight-tag.png' %}
