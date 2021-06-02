---
layout: default
title: Coding Resources
description: Resources curated for coding in general, and also as it relates to health tech.
parent: Resources
nav_order: 1
---

# Coding Resources
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

{% assign resources = site.data.resources | where: 'page', 'Coding' | sort: 'category' %}
{% assign categories = resources | map: 'category' | uniq | sort_natural %}

<div>
{% assign today = site.time | date: '%s' %}
{% for category in categories %}
## {{ category }}
  {% assign subcategories = resources | where: 'category', category | map: 'subcategory' | uniq | sort_natural %}
  {% for subcategory in subcategories %}
### {{ subcategory }}
    {% assign subcategory_resources = resources | where: 'category', category | where: 'subcategory', subcategory | sort: 'name' %}
| Link | Description |
| :--- | :---------- |
    {% for resource in subcategory_resources -%}
| [{{ resource.name }}]({{ resource.url }}) | {% assign start = resource.date | date: '%s' %}{% assign secondsSince = today | minus: start %}{% assign hoursSince = secondsSince | divided_by: 60 | divided_by: 60 %}{% assign daysSince = hoursSince | divided_by: 24 %}{% if daysSince <= 10 %}<span class="label label-green v-align-top">NEW</span>{% endif %}{{ resource.tagline }} |
    {% endfor -%}
  {% endfor %}
  ---
{% endfor %}
</div>
