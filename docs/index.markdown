---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
<!-- Pinned post feature -->

<div class="home">

  <h1 class="page-heading">Posts</h1>

  {% assign pinned_post = site.posts | where: "pinned", true | first %}
  {% assign other_posts = site.posts | where_exp: "post", "post.pinned != true" %}

  <ul class="post-list">
    {% if pinned_post %}
      <li>
        <span class="post-meta">{{ pinned_post.date | date: "%b %-d, %Y" }}</span>
        <h2>
          <a class="post-link" href="{{ pinned_post.url | relative_url }}">{{ pinned_post.title }}</a>
        </h2>
      </li>
    {% endif %}

    {% for post in other_posts %}
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

<!-- Pinned post end -->
