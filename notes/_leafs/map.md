---
layout: page
title: 配信地域
---

<h2>Maps</h2>

<select id="area_box"></select>

<ul id="map_list"></ul>

<div id="map_container">
  <div id="map"></div>
</div>

<script src="https://maps.google.com/maps/api/js?sensor=true&callback=initMap" async defer></script>
<script src="https://cdn.jsdelivr.net/npm/@googlemaps/markermanager/dist/index.umd.min.js"></script>
<script type="text/javascript">
let areas = {
  '日本': [38.474917, 136.549228, 5],
  '北米': [39.878114, -96.629798, 4],
};
document.addEventListener('DOMContentLoaded', () => {
  let elem = document.getElementById('area_box');
  Object.keys(areas).forEach(a => {
    let op = document.createElement('option');
    op.appendChild(document.createTextNode(a));
    elem.appendChild(op);
  });
  elem.addEventListener('change', () => {
    initMap(elem.value);
  }, false);
}, false);
function initMap(ar='日本') {
  let ct = areas[ar];
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
    let ml = document.getElementById('map_list');
    ml.innerHTML = '';
    let list = {{site.maps|jsonify}}.filter(l => {
      return l.area === ar;
    }).filter(l => {
      return (l.cid || l.uid);
    });
    list.sort((a, b) => a.lng < b.lng);
    list.forEach(l => {
      ml.insertAdjacentHTML(
        'beforeend',
        `<li><a href='${baseurl}${l.url}'>${l.title}</a>：${l.tags.join(', ')}</li>`,
      );
    });
    list = list.map(l => {
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
