---
layout: page
title: 配信地域
---

<h2>Maps</h2>
<ul>
  {% for p in site.maps %}
  <li><a href="{{ site.baseurl }}{{ p.url }}">{{ p.title }}</a></li>
  {% endfor %}
</ul>

<div id="map_container">
  <div id="map"></div>
</div>

<script src="https://cdn.jsdelivr.net/npm/@googlemaps/markermanager/dist/index.umd.min.js"></script>
<script type="text/javascript">
function initMap() {
  var map = new google.maps.Map(document.getElementById('map'), {
    center: new google.maps.LatLng(35.474917, 139.549228),
    mapTypeId: google.maps.MapTypeId.ROADMAP,
    zoom: 4,
  });
  var mgr = new google.maps.plugins.markermanager.MarkerManager(map, {});
  google.maps.event.addListener(mgr, 'loaded', function() {
    var list = {{site.maps|jsonify}}.map(l => {
      return new google.maps.Marker({
        position: new google.maps.LatLng(l.lat, l.lng),
        title: l.title,
      });
    });
    mgr.addMarkers(list, 3);
    mgr.refresh();
  });
}
</script>
<script async defer type="text/javascript" src="https://maps.google.com/maps/api/js?sensor=true&callback=initMap"></script>
