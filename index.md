---
title: "Welcome to my blog"
layout: default
---

I'm glad you are here.

I plan to talk mostly about Quantum Mechanics with a layman's attitude.  
Trying to work out how it goes. With ambition of getting it right in the end. Likely I take quite a few incorrect paths on the way.  

So, please have a look on the [Disclaimer](1977/07/22/disclaimer)

Might be I have a few words on ICT as well, probably not as much as a layman at all.  
Without ruling environmental sustainability out.  
And yet, I am a bit afraid I can't help of including some anecdotes from along the road.  
Oh dear, now I had some poems included.  
I am now uncertain whether I can help of not adding whatever categories I feel tempting.  
You'll see it beneath :-)


<ul>
{% for tag in site.tags %}
   <li>
      <a href="#{{ tag[0] }}">{{ tag[0] }}</a>
   </li>
{% endfor %}
</ul>
<HR>

{% assign blog = "../blog" %}
{% if jekyll.environment == "development" %}
{% assign blog = "" %}
{% endif %}


<div style="page-break-after: always; visibility: hidden"> \pagebreak </div>
{% for tag in site.tags %}
  <h3 ID="{{ tag[0] }}">{{ tag[0] }}</h3>
  <ul>
    {% assign sorted_posts = tag[1] | reverse %}
    {% for post in sorted_posts %}
      <li>   	
 		<a href="{{blog}}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
  </ul>
  <HR>
 <div style="page-break-after: always; visibility: hidden"> \pagebreak </div>
{% endfor %}
