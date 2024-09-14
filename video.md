---
layout: page
title: Video
---

<div class="no-select post-card-container">
    {% for post in site.categories.video %}
        {% include /components/cards/post-card.html data=post %}
    {% endfor %}
</div>
