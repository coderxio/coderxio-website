---
layout: page
title: Posts
nav_order: 6
---

# Posts

<ul class="posts">
   {% for post in site.posts %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
   {% endfor %}
</ul>
