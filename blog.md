---
layout: page
title: Blog
permalink: /blog
---

<div class="post-card-container">
    {% for post in site.categories.blog %}
        {% if post.imgUrl %}
            <div class="post-card" onclick="location.href='{{ post.url }}'"
            style="background-image: url({{ post.imgUrl }})">
                <p href="{{ post.url }}">{{ post.title }}</p>
            </div>
        {% else %}
            <div class="post-card" onclick="location.href='{{ post.url }}'"
            style="background-image: url(/assets/img/logo/med-logo-compressed.png)">
                <p href="{{ post.url }}">{{ post.title }}</p>
            </div>
        {% endif %}
    {% endfor %}
</div>
