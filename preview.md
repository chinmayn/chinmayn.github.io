---
layout: preview
title: Template Preview
permalink: /preview/
published: false
---

<section class="tpl-preview">
  <div class="tpl-hero">
    <h1>Modern, clean personal blog template</h1>
    <p>
      This is a design prototype for your eventual refactor: clearer navigation, structured writing feed, and easier topic retrieval.
    </p>

    <div class="tpl-nav">
      <span class="tpl-nav-chip">Home</span>
      <span class="tpl-nav-chip is-active">Writing</span>
      <span class="tpl-nav-chip">Topics</span>
      <span class="tpl-nav-chip">About</span>
      <span class="tpl-nav-chip">Links</span>
    </div>

    <p class="tpl-hero-note">
      This block is only for design preview and will not appear on the final homepage.
    </p>
  </div>

  <section class="tpl-panel">
    <h2>Collections</h2>
    <div class="tpl-collections">
      <span class="tpl-collection-chip"><span class="tpl-glyph">PT</span> Product &amp; Tech</span>
      <span class="tpl-collection-chip"><span class="tpl-glyph">BK</span> Books</span>
      <span class="tpl-collection-chip"><span class="tpl-glyph">MV</span> Movies</span>
      <span class="tpl-collection-chip"><span class="tpl-glyph">TV</span> TV</span>
    </div>
  </section>

  <div class="tpl-grid">
    <section class="tpl-panel tpl-writing">
      <h2>Writing</h2>
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
            <p class="tpl-meta"><span class="tpl-glyph">{{ glyph }}</span> {{ kind }} · {{ post.date | date: "%b %-d, %Y" }}{% if post.tags %} · {{ post.tags | first }}{% endif %}</p>
            <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>
            {% assign card_summary = post.summary | default: post.excerpt %}
            <p>{{ card_summary | strip_html | truncate: 150 }}</p>
          </li>
        {% endfor %}
      </ul>
    </section>
  </div>

  <section class="tpl-panel tpl-topics-compact">
    <h2>Topics</h2>
    <div class="tpl-tags">
      {% assign tags = site.tags | sort %}
      {% for tag in tags %}
        <span class="tpl-tag">{{ tag[0] }} ({{ tag[1] | size }})</span>
      {% endfor %}
    </div>
    <p class="tpl-footer-note">
      Topics stay compact on the Writing page and expand into full browsing on a dedicated Topics page later.
    </p>
  </section>
</section>
