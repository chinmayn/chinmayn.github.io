---
layout: page
permalink: /blog/
title: Welcome to my blog!
---
Hi! I write about things that fascinate me — from deep dives into technology and product strategy to essays on the stories and ideas that shape our culture.

## 📌 Technical & Product Writing
Insights, frameworks, and explorations at the intersection of technology, product management, and real-world impact.

[Read more »](#) <!-- Add your link here -->

## 🎥📚 Reflections & Reviews
Essays about movies, books, TV shows, and other stories — what they reveal, how they linger, and why they matter.

<div class="posts">
  {% assign tagged_posts = site.posts | where_exp:"post","post.tags contains 'pop-culture'" %}
  {% for post in tagged_posts %}
    <h4><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h4>
  {% endfor %}
</div>

---

_Thanks for reading — I hope you find something here that sparks your mind._

