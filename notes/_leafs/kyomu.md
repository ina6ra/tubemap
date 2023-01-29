---
layout: page
title: 虚無シリーズ
---

<h2>バズレシピ</h2>

{% for p in site.kyomu %}
<h2>{{ p.title }}</h2>
<p>
  <a href="{{ site.baseurl }}{{ p.url }}"><img src="{{ p.thumbnail }}" /></a>
</p>
{% endfor %}
