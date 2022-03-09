---
layout: page
title: Posts
nav_order: 6
---
# Posts

We periodically write articles about topics where technology meets healthcare - specifically as it relates to pharmacy and the medication use process.
{: .fs-6 .fw-300 }

<ul class="posts">
   {% for post in site.posts %}
      <li><a href="{{ post.url }}">{{ post.title }}</a></li>
   {% endfor %}
</ul>