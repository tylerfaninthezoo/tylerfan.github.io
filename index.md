welcome to my page

### My Posts

{% for post in site.posts %}
  <article>
    <h2>
        <a href="{{ site.url }}{{ post.url }}">
            {{ post.title }}
        </a>
    </h2>
  </article>
{% endfor %}