---
layout: page
title: Blog
permalink: /blog
---
<div data-nosnippet class="no-select post-card-container">
    {% for post in site.categories.blog %}
        {% include /components/post-card.html data=post %}
    {% endfor %}
</div>
