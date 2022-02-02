---
title: "Welcome to my blog"
---

I'm glad you are here. I plan to talk mostly about Quantum Mechanics with a layman's attitude.
Might be I have a few words on ICT as well, not as a layman at all.


<ul>
  {% for post in site.posts %}
    <li>
      <a href="/blog{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
