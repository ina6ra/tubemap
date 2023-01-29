---
layout: page
title: 虚無シリーズ
---

<h2>バズレシピ</h2>
<ul>
  {% for p in site.kyomu %}
  <li><a href="{{ site.baseurl }}{{ p.url }}">{{ p.title }}</a></li>
  {% endfor %}
</ul>
