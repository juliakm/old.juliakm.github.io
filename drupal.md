---
layout: page
title: Drupal
---

<p class="message">
  This is an archive of my Drupal posts.</p> 


<ul class="posts">
{% for post in site.categories.drupal %}
<li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ post.url }}">{{ post.title }}</a></li>
{% endfor %}
</ul>