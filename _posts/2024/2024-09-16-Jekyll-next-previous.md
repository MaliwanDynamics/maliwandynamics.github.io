---
layout: post

title: Next And Previous Post Previews In Jekyll
imgUrl: /assets/img/post/sept-2024/jekyll-next-prev-direction-head-img.jpg

imgCaption: This Way Dude
imgCaptionSrc: https://www.pexels.com/photo/yellow-arrow-led-signage-394377/

date: 2024-09-16 12:00:00 -0400
categories:
- blog
- software
---

I was having difficulty making a next and previous preview at the end of each post for my site using Jekyll.

The main issue was not that I couldn't make next and previous links, it was that I couldn't find a more concise way to hydrate next and previous cards with an image preview based on the corresponding post. In other words, I wanted to make it pretty.

So after some searching and tinkering I found it was quite simple.

Turns out you can pass the entire `Page` with all its defined values into an includes HTML. Sort-of like passing in an object (I'm guessing) if you are familiar with [Object Oriented Programming (OOP)](https://en.wikipedia.org/wiki/Object-oriented_programming). This way I can grab all the defined values declared within the post inside of a reusable includes.

I'm definitely going to work on making it look better in the future, but it's still a prototype and it works.

## Example

First, evaluate what properties you need for a preview, and what you have commonly defined on each post. All I needed was the title, categories, image/thumbnail, and miscellaneous details like the URL.

This could get a bit more challenging if you need more details than just that in your preview. Maybe I'll figure out a way to extract more data in another post or link to something I find in the future.

Jekyll pages allow you to grab the values from the previous and next post directly from the reference passed into an includes. On the other hand I wanted my includes to be more generic than that. So in this example I am passing in the entirety of the previous and next pages into the includes so that the code does not have to be aware of which page it's on.

I think this allows for a bit more reuse and decouples it from whatever page is implementing the preview functionality so it's not tied directly to this specific use case.

### Example Structure

```
/_post/your-post.md
/_includes/components/post-card.html
/_layouts/post.html
/assets/css/...
```

### your-post.md Example Post Header

This represents a markdown file you have in your `/_post/` directory.

{% raw %}
```html
---
layout: post

title: Jekyll Syntax Highlighting For Code Snippets
imgUrl: /assets/img/post/sept-2024/syntax-highlight-computer-head-img.jpg

date: 2024-09-14 12:00:00 -0400
categories:
- blog
- software
---

Your content typically goes here...

```
{% endraw %}

### Page post.html

Keep in mind you can further extract the includes into something like a `preview-cards.html` and pass in the page there instead of having the if condition in the `post.html` layout. I went this route for now but will probably change it in the future.

{% raw %}
```html
<article class="post-container">

  ...

  <section class="post-content">
    ...
    {{ content }}
  </section>
  <section>
    {% if page.next %}
    {% include /components/post-card.html data=page.next disclaimer="NEXT" %}
    {% endif %}
    {% if page.previous %}
    {% include /components/post-card.html data=page.previous disclaimer="PREVIOUS" %}
    {% endif %}
  </section>

</article>
```
{% endraw %}

### Post Card Preview post-card.html

The `data` field has all the page properties accessible in the includes. If you are not trying to fetch youtube video thumbnails, just remove the condition for `include.data.vidoeId` and everything in it. Just leave the div for `include.data.imgUrl` and replace imgUrl with the defined image field in your post.

{% raw %}
```html
{% if include.data %}
<a class="post-card" href="{{ include.data.url }}" rel="noopener noreferrer" draggable="false">
  <div class="post-card-item">
	{% if include.disclaimer %}<p>{{ include.disclaimer }}</p>{% endif %}
	<p>{{ include.data.title }}</p>
	<p class="generic-date">{{ include.data.date | date: '%-d %B %Y' }}</p>
	<p class="generic-description">{{ include.data.description }}</p>
	<p class="generic-categories">
	{% for cat in include.data.categories %}
  	{{ cat }};
	{% endfor %}
	</p>
  </div>
  {% if include.data.videoId %}
  <div class="post-card-item">
	<div class="post-card-img" style="background-image: url({{ site.yt_img_url_base }}{{ include.data.videoId }}/0.jpg)"></div>
  </div>
  {% else if include.data.imgUrl %}
  <div class="post-card-item">
	<div class="post-card-img" style="background-image: url({{ include.data.imgUrl }})"></div>
  </div>
  {% endif %}
</a>
{% endif %}
```
{% endraw %}

### Post Card SASS

Here is some of the boilerplate CSS I am using for your convenience. It's rather specific to my application and will need to be adjusted to work with your own code.

```css
.post-card-container {
	margin: 0 auto;
}

.post-card {
	display: flex;
	flex-wrap: wrap;

	align-items: center;
	justify-content: center;

	text-decoration: none;
	font-weight: bold;

	width: 100%;
	min-width: 50px;

	height: auto;
	margin-top: 20px;

	color: $master-accent-grey;

	border-top: 1px solid $master-accent-light-grey;
}

.post-card p {
	padding: 0 !important;
}

.post-card:hover {
	background-color: $master-accent;
	color: $master-accent-black;
}

.post-card-item {
	padding: 5px;
	display: inline-block;

	width: calc(100% / 2 - 10px);
	min-width: 200px;
}

.post-card-img {
	width: 100%;
	height: 220px;
	background-size: cover;
	background-repeat: no-repeat;
	background-position: 50% 50%;
}

@media (max-width: 768px) {
	.post-card-item {
    	width: 100%;
	}
}
```

### End Result

With the example above, I now have something like this at the end of every post.

{% include /components/general-figure.html figureImg='/assets/img/post/sept-2024/next-previous-jekyll-preview.png' %}
