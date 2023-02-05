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

<script src="https://maps.google.com/maps/api/js?sensor=true&callback=initMap" async defer></script>
<script src="https://cdn.jsdelivr.net/npm/@googlemaps/markermanager/dist/index.umd.min.js"></script>
<script type="text/javascript">
function initMap(ct=0) {
  let centers = [
    [38.474917, 136.549228, 5],
  ];
  ct = centers[ct];
  let map = new google.maps.Map(document.getElementById('map'), {
    center: new google.maps.LatLng(ct[0], ct[1]),
    mapTypeId: google.maps.MapTypeId.ROADMAP,
    zoom: ct[2],
  });
  let infowindow = null;
  let baseurl = location.href.split(/\//);
  baseurl.pop();
  baseurl = baseurl.join('/');
  let mgr = new google.maps.plugins.markermanager.MarkerManager(map, {});
  google.maps.event.addListener(mgr, 'loaded', () => {
    let list = {{site.maps|jsonify}}.filter(l => {
      return (l.cid || l.uid);
    }).map(l => {
      return {
        lat: l.lat,
        lng: l.lng,
        url: l.url,
        title: l.title,
        tags: l.tags,
      };
    }).map(l => {
      let marker = new google.maps.Marker({
        position: new google.maps.LatLng(l.lat, l.lng),
        title: l.title,
      });
      google.maps.event.addListener(marker, 'click', () => {
        if (infowindow) infowindow.close();
        infowindow = new google.maps.InfoWindow({
          content:`<a href='${baseurl}${l.url}'>${l.title}</a><br>${l.tags}`,
        });
        infowindow.open(map, marker);
      });
      return marker;
    });
    mgr.addMarkers(list, 3);
    mgr.refresh();
  });
}
</script>
