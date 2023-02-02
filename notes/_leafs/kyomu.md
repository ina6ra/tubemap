---
layout: page
title: 虚無レシピ
---

<iframe sandbox="allow-popups allow-scripts allow-modals allow-forms allow-same-origin" style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//rcm-fe.amazon-adsystem.com/e/cm?lt1=_blank&bc1=FFFFFF&IS2=1&bg1=FFFFFF&fc1=000000&lc1=0000FF&t=ina6ra-22&language=ja_JP&o=9&p=8&l=as4&m=amazon&f=ifr&ref=as_ss_li_til&asins=4040650018&linkId=b0dd07ca8e57cadc543d6470f78a66b1"></iframe>

{% assign items = site.kyomu | sort: 'date' | reverse %}
{% for p in items %}
<h2>{{ p.title }}</h2>
<p>
  <a href="{{ site.baseurl }}{{ p.url }}"><img src="{{ p.thumbnail }}" /></a>
</p>
{% endfor %}
