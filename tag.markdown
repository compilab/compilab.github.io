---
layout: page
title: Tags
permalink: /tag/

---

{% for post in site.category %}
       
<ul class="post-list">
    <li>
        <a class="post-link" href="{{ post.url | relative_url }}">
            • {{ post.title | escape }}
        </a>
    </li>
</ul>
{% endfor %}