---
layout: page
title: Archive
permalink: /archive/
---

<div class="home">
  <h1 class="page-heading">Posts</h1>
  <ul>
    {% for post in site.posts %}
      <li>
          <a class="post-link" href="{{ post.url | prepend: site.baseurl }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
</div>

