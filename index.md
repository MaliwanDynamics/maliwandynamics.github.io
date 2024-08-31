---
layout: home
---
<div class="no-select post-card-container" data-nosippet>
    {% for post in site.posts limit: 10 %}
        {% if post.videoId %}
        <a class="post-card" href="{{ post.url }}">
            <div class="post-card-item">
                <p>{{ post.title }}</p>
                <p class="generic-date">{{ post.date | date: '%-d %B %Y' }}</p>
                <p class="generic-categories">{{ post.categories }}</p>
            </div>
            <div class="post-card-item">
                <div class="post-card-img" style="background-image: url({{ site.yt_img_url_base }}{{ post.videoId }}/0.jpg)"></div>
            </div>
        </a>
        {% else %}
        <a class="post-card" href="{{ post.url }}">
            <div class="post-card-item">
                <p>{{ post.title }}</p>
                <p class="generic-date">{{ post.date | date: '%-d %B %Y' }}</p>
                <p class="generic-categories">{{ post.categories }}</p>
            </div>
            <div class="post-card-item">
                <div class="post-card-img" style="background-image: url({{ post.imgUrl }})"></div>
            </div>
        </a>
        {% endif %}
    {% endfor %}
</div>