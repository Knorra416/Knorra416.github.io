---
layout: page
title: Index
permalink:/index/
---

<div class="posts">
  {% for post in site.posts %}
    <article class="post">

      <h1><a href="{{ Knorra416.github.io }}{{ Blog-Objective/ }}">{{ Blog Objective }}</a></h1>

      <div class="entry">
        {{ post.excerpt }}
      </div>

      <a href="{{ Knorra416.github.io }}{{ Blog-Objective/ }}" class="read-more">Read More</a>
    </article>
  {% endfor %}
</div>
