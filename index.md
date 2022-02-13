---
title: "Welcome to my blog"
---

I'm glad you are here.

I plan to talk mostly about Quantum Mechanics with a layman's attitude.  
Might be I have a few words on ICT as well, probably not as much as a layman at all.  
Without ruling environmental sustainability out. 

{% for tag in site.tags %}
  <h3>{{ tag[0] }}</h3>
  <ul>
    {% for post in tag[1] %}
      <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
{% endfor %}
