---
layout: post
title:  "Shells by address"
date:   2014-03-17 11:30:00
---

<html>
  <head>
  <style>
    #map-canvas { width:700px; height:500px; }
    .layer-wizard-search-label { font-family: sans-serif; font-size: 8;};
  </style>
  <script type="text/javascript"
    src="http://maps.google.com/maps/api/js?sensor=false">
  </script>
  <script type="text/javascript">
    var map;
    var layer_0;
    function initialize() {
      map = new google.maps.Map(document.getElementById('map-canvas'), {
        center: new google.maps.LatLng(40, -100),
        zoom: 4
      });
      var style = [
        {
          featureType: 'all',
          elementType: 'all',
          stylers: [
            { saturation: -76 }
          ]
        }
      ];
      var styledMapType = new google.maps.StyledMapType(style, {
        map: map,
        name: 'Styled Map'
      });
      map.mapTypes.set('map-style', styledMapType);
      map.setMapTypeId('map-style');
      layer_0 = new google.maps.FusionTablesLayer({
        query: {
          select: "'Registered Agent'",
          from: "1DFAnYbfnDXzIYgKMDsBdX2otLEpO21kgB-na07b5"
        },
        map: map,
        styleId: 2,
        templateId: 2
      });
    }
    function changeMap_0() {
      var whereClause;
      var searchString = document.getElementById('search-string_0').value.replace(/'/g, "\\'");
      if (searchString != '--Select--') {
        whereClause = "'Type of crime' = '" + searchString + "'";
      }
      layer_0.setOptions({
        query: {
          select: "'Registered Agent'",
          from: "1DFAnYbfnDXzIYgKMDsBdX2otLEpO21kgB-na07b5",
          where: whereClause
        }
      });
    }
    google.maps.event.addDomListener(window, 'load', initialize);
  </script>
  </head>
  <body>
    <div id="map-canvas"></div>
    <div style="margin-top: 10px;">
      <label class="layer-wizard-search-label">
        <span style='font-size:10'>Type of crime to display on map</span>
        <select id="search-string_0" onchange="changeMap_0(this.value);">
          <option value="--Select--">--Select--</option>
          <option value="Defrauding government to obtain contracts">Defrauding government to obtain contracts</option>
          <option value="Medicare fraud">Medicare fraud</option>
          <option value="Money laundering for illegal arms trade">Money laundering for illegal arms trade</option>
          <option value="Money laundering for illegal drugs operation">Money laundering for illegal drugs operation</option>
          <option value="Money laundering for smuggling">Money laundering for smuggling</option>
        </select>
      </label> 
    </div>
  </body>
</html>
