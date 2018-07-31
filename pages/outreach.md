---
layout: page
show_meta: false
title: "Outreach"
subheadline: "Some articles I wrote on other sites"
header:
   image_fullwidth: "header_unsplash_5.jpg"
permalink: "/outreach/"
---
<ul>
    {% for post in site.categories.outreach %}
    <li><a href="{{ site.url }}{{ post.url }}">{{ post.title }}</a></li>
    {% endfor %}
</ul>
