---
layout: page
title: Chenfeng ZHU (朱辰丰)
tagline: Welcome to My World!
---
{% include JB/setup %}

Hi, I am Chenfeng ZHU (朱辰丰).

Here is my world. Take a tour to look around and find something you are interested in.

<ul class="post-list">
  {% for post in site.posts limit:5 %}
    <li>
      <h2>
        <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      </h2>
      <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
      <p>
        {% if post.abstract %}
          {{ post.abstract | strip_html | xml_escape | truncatewords: 50 }}
        {% else %}
          {{ post.content | strip_html | xml_escape | truncatewords: 50 }}
        {% endif%}
      </p>
    </li>
  {% endfor %}
</ul>

