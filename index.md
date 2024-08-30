---
layout: home
---

<div class="post-card-container">
    {% for post in site.posts limit: 3 %}
        {% if post.videoId %}
            <div class="post-card" onclick="location.href='{{ post.url }}'"
            style="background-image: url({{ site.yt_img_url_base }}{{ post.videoId }}/0.jpg)">
                <p href="{{ post.url }}">{{ post.title }}</p>
            </div>
        {% else %}
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
        {% endif %}
    {% endfor %}
</div>
