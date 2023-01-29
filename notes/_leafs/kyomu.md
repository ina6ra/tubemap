---
layout: page
title: 虚無シリーズ
---

<h2>バズレシピ</h2>

{% assign items = site.kyomu | sort: 'date' | reverse %}
{% for p in items %}
<h2>{{ p.title }}</h2>
<p>
  <a href="{{ site.baseurl }}{{ p.url }}"><img src="{{ p.thumbnail }}" /></a>
</p>
{% endfor %}
