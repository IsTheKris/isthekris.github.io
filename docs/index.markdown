---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
<div class="home">

  <!-- Show pinned post(s) first -->
  {% assign pinned_posts = site.posts | where: "pinned", true %}
  {% for post in pinned_posts %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    {{ post.excerpt }}
    <hr />
  {% endfor %}

  <!-- Then show other (unpinned) posts -->
  {% assign unpinned_posts = site.posts | where_exp: "post", "post.pinned != true" %}
  {% for post in unpinned_posts %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    {{ post.excerpt }}
    <hr />
  {% endfor %}

</div>
