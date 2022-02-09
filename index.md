---
title: "Welcome to my blog"
---

I'm glad you are here.

I plan to talk mostly about Quantum Mechanics with a layman's attitude.  
Might be I have a few words on ICT as well, probably not as much as a layman at all.  
Without ruling environmental sustainability out. 


<ul>
  {% for post in site.posts %}
    <li>
      <a href="/blog{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
