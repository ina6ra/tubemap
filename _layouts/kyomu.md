---
layout: default
---

<h2>{{ page.title }}</h2>

{% if page.width %}
<div style="width: {{page.width}}; margin:0 auto;">
{% else %}
<div>
{% endif %}
  <div class="ytcontainer">
    <iframe class="yt" allowfullscreen src="https://www.youtube.com/embed/{{page.vid}}"></iframe>
  </div>
</div>
