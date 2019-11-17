---
layout: page
title: "About"
description: "Who am I?"
header-img: "img/home-bg.jpg"
---


<!--
<meta http-equiv="refresh" content="0;url='https://voidism.github.io/home'">
![Jexus](../img/Jexus.jpg)# Yung-Sung Chuang  
Undergraduate Student / Electrical Engineering

Hi! My name is Yung-Sung Chuang, a student who major in electrical engineering in National Taiwan University.
I will share some notes or articles during my study. Thanks for reading and taking the time to comment :)
-->
<hr>

{% for member in site.data.members %} {% if member.visible == true %}

<img src="{{ member.img }}" style="margin-top:0px; margin-bottom:5px; margin-right:10px; float:left; width:150px !important">

<h1>{{ member.name }}</h1>

<h3>{{ member.role }}</h3>

{% if member.github %} 
<span class="social-share-googleplus"><a href="https://github.com/{{ member.github }}" title="Github"><img src="{{ "/img/icons/github-icon.png" | prepend: site.baseurl }}" style="height:20px">Github</a></span> 
{% endif %}
{% if member.gplus %}
<span class="social-share-googleplus"><a href="{{ member.gplus }}" title="Google Plus"><img src="{{ "/img/icons/gplus-icon.png" | prepend: site.baseurl }}" style="height:20px">Google Plus</a></span>
{% endif %}
{% if member.url %}
<span class="social-share-googleplus"><a href="{{ member.url }}" title="Google Plus"><img src="{{ "/img/icons/url-icon.png"| prepend: site.baseurl }}" style="height:20px">Website</a></span>
{% endif %}
{% if member.email %}
<span class="social-share-googleplus"><a href="{{ member.email }}" title="E-mail"><img src="{{ "/img/icons/email-icon.jpg" | prepend: site.email }}" style="height:20px">E-mail</a></span>
{% endif %}

{% if member.bio %} 
{{ member.bio }}
{% endif %}

E-mail: b05901033[at]ntu.edu.tw

<hr>

{% endif %}{% endfor %}
	