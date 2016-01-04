---
layout: page
title: Archive
permalink: /archive/
---

<div class="home">
  <ul>
    {% for post in site.posts %}
      <li>
          <a href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
</div>

