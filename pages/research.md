---
layout: page
show_meta: false
title: "Research"
subheadline: ""
header:
   image_fullwidth: "header_unsplash_5.jpg"
permalink: "/research/"
---
<!-- <ul>
    {% for post in site.categories.research %}
    <li><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul> -->



{% for post in site.categories.research %}
<hr />
<div class="row">
  <div class="small-3 columns">
    {% if post.thumbnail %}
	<img src="{{ post.thumbnail }}" align="center" width="150" />
	{% else %}
	<img src="/assets/img/nature.png" align="center" width="150"/>
	{% endif %}
  </div>
  <div class="small-9 columns">
  <a href="{{ post.url }}"><h3>{{ post.title }}</h3></a>
  <p>{{ post.subheadline }}</p>
	<p>{{ post.content | strip_html | truncatewords: 40 }}
	</p>
  </div>
</div>
{% endfor %}
