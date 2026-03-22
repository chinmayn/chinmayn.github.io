---
layout: page
permalink: /blog/
title: Writing
---

<p class="writing-intro">
  Essays and notes across product, technology, and culture.
</p>

<div class="writing-filter" aria-label="Filter writing by tag">
  <button class="writing-filter-chip is-active" data-tag="all" type="button">All</button>
  {% assign all_tags = site.tags | sort %}
  {% for tag in all_tags %}
    <button class="writing-filter-chip" data-tag="{{ tag[0] | slugify }}" type="button">{{ tag[0] }}</button>
  {% endfor %}
</div>

{% assign pt_posts = site.posts | where: "type", "product-tech" %}
{% assign reflection_posts = site.posts | where: "type", "reflections" %}
{% assign note_posts = site.posts | where: "type", "notes" %}
{% assign other_posts = site.posts | where_exp: "post", "post.type != 'product-tech'" %}
{% assign other_posts = other_posts | where_exp: "post", "post.type != 'reflections'" %}
{% assign other_posts = other_posts | where_exp: "post", "post.type != 'notes'" %}

{% if pt_posts.size > 0 %}
  <section class="writing-section" data-writing-section>
    <h2 class="writing-section-title">Product &amp; Tech</h2>
    <div class="writing-list">
      {% for post in pt_posts %}
        {% assign tags_attr = post.tags | join: "," | downcase | replace: " ", "-" %}
        <article class="writing-card" data-tags="{{ tags_attr }}">
          <p class="writing-meta">
            <span class="writing-glyph">PT</span>
            <span>Product &amp; Tech</span>
            <span>&middot;</span>
            <span>{{ post.date | date: "%b %-d, %Y" }}</span>
          </p>
          <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>
          {% assign card_summary = post.summary | default: post.excerpt %}
          <p>{{ card_summary | strip_html | truncate: 180 }}</p>
          {% if post.tags and post.tags.size > 0 %}
            <div class="writing-card-tags">
              {% for tag in post.tags %}
                <span class="writing-card-tag">{{ tag }}</span>
              {% endfor %}
            </div>
          {% endif %}
        </article>
      {% endfor %}
    </div>
  </section>
{% endif %}

{% if reflection_posts.size > 0 %}
  <section class="writing-section" data-writing-section>
    <h2 class="writing-section-title">Reflections &amp; Reviews</h2>
    <div class="writing-list">
      {% for post in reflection_posts %}
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
        {% assign tags_attr = post.tags | join: "," | downcase | replace: " ", "-" %}
        <article class="writing-card" data-tags="{{ tags_attr }}">
          <p class="writing-meta">
            <span class="writing-glyph">{{ glyph }}</span>
            <span>{{ kind }}</span>
            <span>&middot;</span>
            <span>{{ post.date | date: "%b %-d, %Y" }}</span>
          </p>
          <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>
          {% assign card_summary = post.summary | default: post.excerpt %}
          <p>{{ card_summary | strip_html | truncate: 180 }}</p>
          {% if post.tags and post.tags.size > 0 %}
            <div class="writing-card-tags">
              {% for tag in post.tags %}
                <span class="writing-card-tag">{{ tag }}</span>
              {% endfor %}
            </div>
          {% endif %}
        </article>
      {% endfor %}
    </div>
  </section>
{% endif %}

{% if note_posts.size > 0 %}
  <section class="writing-section" data-writing-section>
    <h2 class="writing-section-title">Notes</h2>
    <div class="writing-list">
      {% for post in note_posts %}
        {% assign tags_attr = post.tags | join: "," | downcase | replace: " ", "-" %}
        <article class="writing-card" data-tags="{{ tags_attr }}">
          <p class="writing-meta">
            <span class="writing-glyph">NT</span>
            <span>Notes</span>
            <span>&middot;</span>
            <span>{{ post.date | date: "%b %-d, %Y" }}</span>
          </p>
          <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>
          {% assign card_summary = post.summary | default: post.excerpt %}
          <p>{{ card_summary | strip_html | truncate: 180 }}</p>
          {% if post.tags and post.tags.size > 0 %}
            <div class="writing-card-tags">
              {% for tag in post.tags %}
                <span class="writing-card-tag">{{ tag }}</span>
              {% endfor %}
            </div>
          {% endif %}
        </article>
      {% endfor %}
    </div>
  </section>
{% endif %}

{% if other_posts.size > 0 %}
  <section class="writing-section" data-writing-section>
    <h2 class="writing-section-title">Other</h2>
    <div class="writing-list">
      {% for post in other_posts %}
        {% assign tags_attr = post.tags | join: "," | downcase | replace: " ", "-" %}
        <article class="writing-card" data-tags="{{ tags_attr }}">
          <p class="writing-meta">
            <span class="writing-glyph">OT</span>
            <span>Other</span>
            <span>&middot;</span>
            <span>{{ post.date | date: "%b %-d, %Y" }}</span>
          </p>
          <h3><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></h3>
          {% assign card_summary = post.summary | default: post.excerpt %}
          <p>{{ card_summary | strip_html | truncate: 180 }}</p>
          {% if post.tags and post.tags.size > 0 %}
            <div class="writing-card-tags">
              {% for tag in post.tags %}
                <span class="writing-card-tag">{{ tag }}</span>
              {% endfor %}
            </div>
          {% endif %}
        </article>
      {% endfor %}
    </div>
  </section>
{% endif %}

<script>
  (function () {
    const chips = Array.from(document.querySelectorAll(".writing-filter-chip"));
    const cards = Array.from(document.querySelectorAll(".writing-card"));
    const sections = Array.from(document.querySelectorAll("[data-writing-section]"));
    if (!chips.length || !cards.length) return;

    function applyFilter(tag) {
      cards.forEach((card) => {
        const tags = (card.getAttribute("data-tags") || "").split(",").filter(Boolean);
        const visible = tag === "all" || tags.includes(tag);
        card.classList.toggle("is-hidden", !visible);
      });

      sections.forEach((section) => {
        const visibleCards = section.querySelectorAll(".writing-card:not(.is-hidden)").length;
        section.classList.toggle("is-hidden", visibleCards === 0);
      });

      chips.forEach((chip) => {
        chip.classList.toggle("is-active", chip.getAttribute("data-tag") === tag);
      });
    }

    chips.forEach((chip) => {
      chip.addEventListener("click", () => {
        const tag = chip.getAttribute("data-tag") || "all";
        const url = new URL(window.location.href);
        if (tag === "all") {
          url.searchParams.delete("tag");
        } else {
          url.searchParams.set("tag", tag);
        }
        history.replaceState(null, "", url.toString());
        applyFilter(tag);
      });
    });

    const startTag = new URLSearchParams(window.location.search).get("tag") || "all";
    const validTag = chips.some((chip) => chip.getAttribute("data-tag") === startTag) ? startTag : "all";
    applyFilter(validTag);
  })();
</script>
