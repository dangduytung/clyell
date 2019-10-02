---
title: "Command"
permalink: /command/
---

<ul class="posts">
    {% for post in site.categories.command %}
        <li>
            <a class="post-link" href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
        </li>
    {% endfor %}
</ul>