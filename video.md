---
layout: page
title: Video
permalink: /video
---

<div class="no-select post-card-container">
    {% for post in site.categories.video %}
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
    {% endfor %}
</div>
