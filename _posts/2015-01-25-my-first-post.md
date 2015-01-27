---
layout: default
title: This is my first post.
---

This is my first post.

Here comes the second paragraph.

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      {{ post.excerpt }}
    </li>
  {% endfor %}
</ul>

