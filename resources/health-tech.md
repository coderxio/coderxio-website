---
layout: default
title: Health Tech Resources
description: Resources curated for health tech.
parent: Resources
nav_order: 3
---

# Health Tech Resources
{: .no_toc }

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---
 
{% assign resources = site.data.resources | where: 'page', 'Health Tech' | sort: 'category' %}
{% assign categories = resources | map: 'category' | uniq | sort_natural %}

<div>
{% for category in categories %}
## {{ category }}
  {% assign subcategories = resources | where: 'category', category | map: 'subcategory' | uniq | sort_natural %}
  {% for subcategory in subcategories %}
### {{ subcategory }}
    {% assign subcategory_resources = resources | where: 'category', category | where: 'subcategory', subcategory | sort: 'name' %}
| Link | Description |
| :--- | :---------- |
    {% for resource in subcategory_resources -%}
| [{{ resource.name }}]({{ resource.url }}) | {{ resource.tagline }} |
    {% endfor -%}
  {% endfor %}
  ---
{% endfor %}
</div>
 