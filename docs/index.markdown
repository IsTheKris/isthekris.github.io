---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

<div class="home">

  <h1 class="page-heading">Posts</h1>

  {% assign pinned = site.posts | where: "pinned", true %}
  {% assign unpinned = site.posts | where_exp: "post", "post.pinned != true" %}

  {% assign sorted_posts = pinned | concat: unpinned %}

  <ul class="post-list">
    {% for post in sorted_posts %}
      <li>
        <span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span>
        <h2>
          <a class="post-link" href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </h2>
      </li>
    {% endfor %}
  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>
</div>
