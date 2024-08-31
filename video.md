---
layout: page
title: Video
permalink: /video
---

<div class="no-select post-card-container">
    {% for post in site.categories.video %}
    <div class="post-card" onclick="location.href='{{ post.url }}'"
    style="background-image: url({{ site.yt_img_url_base }}{{ post.videoId }}/0.jpg)">
        <p href="{{ post.url }}">{{ post.title }}</p>
    </div>
    {% endfor %}
</div>
