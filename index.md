---
layout: default
permalink: /
title: Home
---

<section class="home-hero">
  <h1>Hi, I’m Chinmay.</h1>
  <p>
    I write concise essays on product, AI, and culture. The goal is simple: clear thinking, practical ideas, and reflections that stay with you.
  </p>
</section>

<section class="home-latest">
  <h2>Latest Writing</h2>
  <div class="writing-list">
    {% for post in site.posts limit: 4 %}
      {% assign kind = "Essay" %}
      {% assign glyph = "ES" %}
      {% if post.tags contains "movie" %}
        {% assign kind = "Movie" %}
        {% assign glyph = "MV" %}
      {% elsif post.tags contains "book" %}
        {% assign kind = "Book" %}
        {% assign glyph = "BK" %}
      {% elsif post.tags contains "tv" %}
        {% assign kind = "TV" %}
        {% assign glyph = "TV" %}
      {% elsif post.type == "product-tech" %}
        {% assign kind = "Product & Tech" %}
        {% assign glyph = "PT" %}
      {% endif %}

      <article class="writing-card">
        <p class="writing-meta">
          <span class="writing-glyph">{{ glyph }}</span>
          <span>{{ kind }}</span>
          <span>&middot;</span>
          <span>{{ post.date | date: "%b %-d, %Y" }}</span>
        </p>
        <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>
        {% assign card_summary = post.summary | default: post.excerpt %}
        <p>{{ card_summary | strip_html | truncate: 160 }}</p>
      </article>
    {% endfor %}
  </div>
</section>
