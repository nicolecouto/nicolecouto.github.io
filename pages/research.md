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
