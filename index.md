---
layout: home
---
<div data-nosnippet class="no-select post-card-container">
    {% for post in site.posts limit: 10 %}
        {% include components/cards/post-card.html data=post %}
    {% endfor %}
</div>