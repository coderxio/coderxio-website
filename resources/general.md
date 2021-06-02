---
layout: default
title: General Resources
description: Resources that haven't been filed away into a more specific section.
parent: Resources
nav_order: 4
---

# General Resources
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

{% assign resources = site.data.resources | where: 'page', 'General' | sort: 'category' %}
{% assign categories = resources | map: 'category' | uniq | sort_natural %}

<div>
{% assign today = site.time | date: '%s' %}
{% for category in categories %}
## {{ category }}
  {% assign subcategories = resources | where: 'category', category | map: 'subcategory' | uniq | sort_natural %}
  {% for subcategory in subcategories %}
### {{ subcategory }}
    {% assign subcategory_resources = resources | where: 'category', category | where: 'subcategory', subcategory | sort: 'name' %}
    {% assign start = resource.date | date: '%s' %}
    {% assign secondsSince = today | minus: start %}
    {% assign hoursSince = secondsSince | divided_by: 60 | divided_by: 60 %}
    {% assign daysSince = hoursSince | divided_by: 24 %}
| Link | Description |
| :--- | :---------- |
    {% for resource in subcategory_resources -%}
| {% if daysSince <= 10 %}<span class="label label-green v-align-top">NEW</span> {% endif %}[{{ resource.name }}]({{ resource.url }}) | {{ resource.tagline }} |
    {% endfor -%}
  {% endfor %}
  ---
{% endfor %}
</div>
