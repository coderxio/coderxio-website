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
[Subscribe](https://mailchi.mp/ac1988c7d7f4/trujlqmy5g) to our mailing list and get a [free CodeRx course](https://mailchi.mp/ac1988c7d7f4/trujlqmy5g) on a beginner's guide to creating and hosting an online CV with GitHub.

We are currently working on several open source [projects](/projects), creating [guides](/guides) to some common sources of health tech data, terminologies, and frameworks, compiling [resources](/resources) for different areas of tech in general and health tech specifically, and publishing [posts](/posts) about topics relating to pharmacy and technology.

Check out our [GitHub repos](https://github.com/coderxio), join our [Slack channel](https://coderx.slack.com), or stop by our [about](/about) page to learn more and get involved.

Have a question?  Just shoot us an [email](mailto:info@coderx.io).

## Projects
* [DailyMed API Project](/projects/dailymed-api)
* [DailyMed UI Project](/projects/dailymed-ui)
* [OpenFDA Project](/projects/openfda)

## Guides
* [DailyMed Guide](/guides/dailymed)

## Resources
* [General Resources](/resources/general)

## Posts
<ul class="posts">
   {% assign today = site.time | date: '%s' %}
   {% for post in site.posts %}
      {% assign start = post.date | date: '%s' %}
      {% assign secondsSince = today | minus: start %}
      {% assign hoursSince = secondsSince | divided_by: 60 | divided_by: 60 %}
      {% assign daysSince = hoursSince | divided_by: 24 %}
      <li>
         <a href="{{ post.url }}">{{ post.title }}</a>
         {% if daysSince <= 10 %}
            <span class="label label-green v-align-top">NEW</span>
         {% endif %}   
      </li>
   {% endfor %}
</ul>
