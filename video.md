---
layout: page
title: Video
permalink: /video
---

<div class="no-select post-card-container">
    {% for post in site.categories.video %}
        {% include /components/post-card.html data=post %}
    {% endfor %}
</div>
