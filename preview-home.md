---
layout: preview
title: Home Template Preview
permalink: /preview-home/
published: false
---

<section class="tpl-preview">
  <div class="tpl-panel">
    <p class="tpl-kicker">Header Option A (Recommended)</p>
    <header class="tpl-site-header">
      <div class="tpl-brand">
        <h1>Chinmay Nivargi</h1>
        <p>Product manager. Writing about product, AI, and culture.</p>
      </div>
      <nav class="tpl-site-nav">
        <span class="is-active">Home</span>
        <span>Writing</span>
        <span>Topics</span>
        <span>About</span>
      </nav>
    </header>
  </div>

  <div class="tpl-panel">
    <p class="tpl-kicker">Header Option B (Avatar Included)</p>
    <header class="tpl-site-header tpl-site-header-avatar">
      <div class="tpl-brand-wrap">
        <img src="{{ site.baseurl }}/images/firestarter.jpeg" alt="Profile photo" class="tpl-avatar" />
        <div class="tpl-brand">
          <h1>Chinmay Nivargi</h1>
          <p>Product manager. Writing about product, AI, and culture.</p>
        </div>
      </div>
      <nav class="tpl-site-nav">
        <span class="is-active">Home</span>
        <span>Writing</span>
        <span>Topics</span>
        <span>About</span>
      </nav>
    </header>
  </div>

  <div class="tpl-hero">
    <h1>Hi, I’m Chinmay.</h1>
    <p>
      I write concise essays on product thinking, AI, and stories from books, movies, and TV. This homepage intro stays short by design.
    </p>
    <div class="tpl-nav">
      <span class="tpl-nav-chip is-active">Read Writing</span>
      <span class="tpl-nav-chip">About Me</span>
    </div>
  </div>

  <section class="tpl-panel">
    <h2>Latest Writing</h2>
    <ul class="tpl-list">
      {% for post in site.posts %}
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
        {% endif %}
        <li class="tpl-item">
          <p class="tpl-meta"><span class="tpl-glyph">{{ glyph }}</span> {{ kind }} · {{ post.date | date: "%b %-d, %Y" }}</p>
          <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>
          {% assign card_summary = post.summary | default: post.excerpt %}
          <p>{{ card_summary | strip_html | truncate: 150 }}</p>
        </li>
      {% endfor %}
    </ul>
  </section>
</section>
