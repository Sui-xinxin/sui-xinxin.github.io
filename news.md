---
layout: default
title: News
---
<script src="https://unpkg.com/masonry-layout@4/dist/masonry.pkgd.min.js"></script>
<script src="https://unpkg.com/imagesloaded@5/imagesloaded.pkgd.min.js"></script>

<style>
.news-grid {
  position: relative;
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 20px;
}

.news-card {
  width: 340px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 16px;
  box-shadow: 2px 2px 6px rgba(0,0,0,0.05);
  background-color: #fff;
}

.news-card img {
  width: 100%;
  height: auto;
  border-radius: 5px;
  margin-bottom: 10px;
}
.news-card-title {
  font-weight: bold;
  font-size: 1.1em;
  margin-bottom: 6px;
}
.news-card-date {
  font-size: 0.9em;
  color: #666;
  margin-bottom: 6px;
}
</style>

<div class="news-grid">
{% assign sorted_news = site.news | sort: 'date' | reverse %}
{% for item in sorted_news %}
  <div class="news-card" id="{{ item.slug }}">
    {% if item.image_link %}
    <a href="{{ item.image_link }}" target="_blank">
      <img src="{{ item.image }}" alt="{{ item.alt | default: item.title }}">
    </a>
    {% else %}
    <img src="{{ item.image }}" alt="{{ item.alt | default: item.title }}">
    {% endif %}
    <div class="news-card-title">{{ item.title }}</div>
    <div class="news-card-date">{{ item.date | date: "%B %-d, %Y" }}</div>
    <p>{{ item.content }}</p>
  </div>
{% endfor %}
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
  var grid = document.querySelector('.news-grid');
  imagesLoaded(grid, function() {
    var msnry = new Masonry(grid, {
      itemSelector: '.news-card',
      columnWidth: '.news-card',
      gutter: 20,
      horizontalOrder: true
    });
  });
});
</script>
---
