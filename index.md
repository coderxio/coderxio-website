---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Home
nav_order: 1
permalink: /
---

# Pharmacists who code
{: .fs-9 }

CodeRx is a collective of pharmacists and other healthcare professionals who have a skill set in tech and apply it towards building useful things.
{: .fs-6 .fw-300 }

[Get started now](#getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [View on GitHub](https://github.com/coderxio){: .btn .fs-5 .mb-4 .mb-md-0 }
---

## Getting started
Check out our [GitHub repos](https://github.com/coderxio) or join our [Slack channel](https://coderx.slack.com) to learn more.

## Projects
<ul>
   <li><a href="/projects/dailymed-api">DailyMed API</a></li>
   <li><a href="/projects/dailymed-ui">DailyMed UI</a></li>
</ul>

## Posts
<ul class="posts">
   {% for post in site.posts %}
      <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
   {% endfor %}
</ul>