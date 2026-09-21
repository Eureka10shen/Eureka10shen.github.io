---
layout: archive
title: "Blog"
permalink: /blog/
author_profile: true
---

This is a collection of technical notes on quantum chemistry, scientific computing, and related topics.

{% assign posts_by_date = site.posts | sort: "date" | reverse %}
{% for post in posts_by_date %}
  {% include archive-single.html %}
{% endfor %}
