---
layout: page
title: News
permalink: /news/
description: Papers, talks and group updates.
---

<ul class="dm-news dm-news-full">
  {% assign news = site.news | reverse %}
  {% for item in news %}
    <li>
      <time datetime="{{ item.date | date_to_xmlschema }}">{{ item.date | date: '%b %Y' }}</time>
      <span>{% if item.inline %}{{ item.content | remove: '<p>' | remove: '</p>' | strip }}{% else %}<a href="{{ item.url | relative_url }}">{{ item.title }}</a>{% endif %}</span>
    </li>
  {% endfor %}
</ul>
