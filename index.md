---
layout: default
---

<body>
  <div class="index-wrapper">
    <div class="aside">
      <div class="info-card">
        <h1>Dzreal</h1>
        <a href="https://github.com/GitDzreal93" target="_blank"><img src="https://github.com/favicon.ico" alt="" width="25"/></a>
      
      <div id="categories-dz" class="left">
        <h2>Categories</h2>
        <ul>
          {% for cat in site.categories %}
            {{ cat[0] }}
          {% endfor %}
        </ul>
      </div>
    <!-- </div>
      <div id="particles-js"></div>
    </div> -->
    <div class="index-content">
      <ul class="artical-list">
        {% for post in site.categories.blog %}
        <li>
          <a href="{{ post.url }}" class="title">{{ post.title }}</a>
          <div class="title-desc">{{ post.description }}</div>
        </li>
        {% endfor %}
      </ul>
    </div>
  </div>
</body>
