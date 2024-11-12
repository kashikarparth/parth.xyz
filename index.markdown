---
layout: default
title: parth.xyz
---

personal notepad

---

{% assign tech_posts_exist = false %}
{% assign thoughts_posts_exist = false %}

{% for post in site.posts %}
{% if post.categories contains "tech" %}
{% assign tech_posts_exist = true %}
{% endif %}
{% if post.categories contains "thoughts" %}
{% assign thoughts_posts_exist = true %}
{% endif %}
{% endfor %}

{% if tech_posts_exist or thoughts_posts_exist %}
{% if tech_posts_exist %}

<h3>posts</h3>

<table>
<tr>
<th>idx</th>
<th>title</th>
</tr>
{% for post in site.posts %}
{% if post.categories contains "tech" %}
<tr>
<td>{{ post.date | date: "%Y%m%d" }}</td>
<td><a href="{{ post.url | relative_url }}">{{ post.title }}</a></td>
</tr>
{% endif %}
{% endfor %}
</table>
{% endif %}

{% if thoughts_posts_exist %}

<h3>thoughts</h3>

<table>
<tr>
<th>idx</th>
<th>title</th>
</tr>
{% for post in site.posts %}
{% if post.categories contains "thoughts" %}
<tr>
<td>{{ post.date | date: "%Y%m%d" }}</td>
<td><a href="{{ post.url | relative_url }}">{{ post.title }}</a></td>
</tr>
{% endif %}
{% endfor %}
</table>
{% endif %}
{% endif %}
