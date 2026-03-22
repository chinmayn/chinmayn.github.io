---
layout: page
title: Topics
permalink: /topics/
---

<p class="topics-intro">
  Browse writing by topic. Each tag groups all related posts.
</p>

<div class="topics-cloud">
  {% assign sorted_tags = site.tags | sort %}
  {% for topic in sorted_tags %}
    <a href="#{{ topic[0] | slugify }}" class="topics-cloud-tag">{{ topic[0] }} ({{ topic[1] | size }})</a>
  {% endfor %}
</div>

{% for topic in sorted_tags %}
  <section id="{{ topic[0] | slugify }}" class="topic-section">
    <h2>{{ topic[0] }} <span class="topic-count">({{ topic[1] | size }})</span></h2>
    <ul class="topic-post-list">
      {% assign posts_for_topic = topic[1] | sort: "date" | reverse %}
      {% for post in posts_for_topic %}
        <li>
          <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
          <span class="topic-date">{{ post.date | date: "%b %-d, %Y" }}</span>
        </li>
      {% endfor %}
    </ul>
  </section>
{% endfor %}
