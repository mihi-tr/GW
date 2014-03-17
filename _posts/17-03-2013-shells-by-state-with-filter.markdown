---
layout: post
title:  "Shells by state with filter"
date:   2014-03-17 11:30:00
---
<html>
  <head>
  <style>
    #map-canvas { width:700px; height:500px; }
    .layer-wizard-search-label { font-family: sans-serif };
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
        zoom: 3
      });
      var style = [
        {
          featureType: 'all',
          elementType: 'all',
          stylers: [
            { saturation: -44 }
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
          select: "col2",
          from: "19pkvbmxGLgkuTMG_3rSmnYulZaOb5JjmOGoJMClz",
          where: " col1 in ('Nebraska', 'Delaware', 'Florida', 'New Jersey', 'Colorado', 'Illinois', 'Louisiana', 'Massachusetts', 'Oregon')"
        },
        map: map,
        styleId: 9,
        templateId: 13
      });
    }
    function changeMap_0() {
      var whereClause = " col1 in ('Nebraska', 'Delaware', 'Florida', 'New Jersey', 'Colorado', 'Illinois', 'Louisiana', 'Massachusetts', 'Oregon')";
      var searchString = document.getElementById('search-string_0').value.replace(/'/g, "\\'");
      if (searchString != '--Select--') {
        whereClause += " AND 'Type of crime facilitated' CONTAINS IGNORING CASE '" + searchString + "'";
      }
      layer_0.setOptions({
        query: {
          select: "col2",
          from: "19pkvbmxGLgkuTMG_3rSmnYulZaOb5JjmOGoJMClz",
          where: whereClause
        }
      });
    }
    google.maps.event.addDomListener(window, 'load', initialize);
  </script>
  </head>
  <body>
    <div id="map-canvas"></div>
    <div style="margin-top: 10px; font-size: 10px; margin-bottom: 10px;">
      <label class="layer-wizard-search-label">
        Filter by type of crime facilitated
        <select id="search-string_0" onchange="changeMap_0(this.value);">
          <option value="--Select--">--Select--</option>
          <option value="Drugs">Drugs</option>
		  <option value="Money laundering">Money laundering</option>
		  <option value="Illegal arms trading">Illegal arms trading</option>
        </select>
      </label> 
    </div>
	<div id="Links"><a href= >View and download the full set of case studies here</a></div>
  </body>
</html>
