---
layout: page
title: Blog
permalink: /blog
---
<div class="no-select post-card-container">
    {% for post in site.categories.blog %}
        {% if post.imgUrl %}
        <a class="post-card" href="{{ post.url }}">
            <div class="post-card-item">
                <p>{{ post.title }}</p>
            </div>
            <div class="post-card-item">
                <div class="post-card-img" style="background-image: url({{ post.imgUrl }})"></div>
            </div>
        </a>
        {% endif %}
    {% endfor %}
</div>
