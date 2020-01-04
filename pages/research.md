---
layout: page
show_meta: false
title: "Research"
subheadline: ""
header:
   image_fullwidth: "header_unsplash_5.jpg"
permalink: "/research/"
---
<ul>
    {% for post in site.categories.research %}
    <li><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>



<!-- {% for post in site.categories.research limit:15 offset:3 %}
<hr />
<div class="row">
  <div class="span2">
    {% if post.thumbnail %}
	<img src="{{ post.thumbnail }}" align="center" />
	{% else %}
	<img src="/assets/img/nature.png" align="center" />
	{% endif %}
  </div>
  <div class="span10">
    <p><a href="{{ post.subheadline }}{{ post.url }}"><h3>{{ post.title }}</h3></a></p>
	<p>{{ post.content | strip_html | truncatewords: 40 }}
	</p>
  </div>
</div>
{% endfor %} -->
