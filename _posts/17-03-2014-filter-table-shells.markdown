---
layout: post
title:  "Filter table shells"
date:   2014-03-17 21:07:00
---

<html>
  <head>
    <meta charset="UTF-8">
	<title>Filter Shell Chart</title>
    <link href="http://www.google.com/uds/api/visualization/1.0/4ea8b4974b307a4ef65cf50fe2dc4df2/table+en.css"
         rel="stylesheet" type="text/css">
    <script type="text/javascript" src="http://www.google.com/jsapi"></script>
	<style type="text/css">
      table {
        width: 30%;
      }

      th {
        width: 30%;
        text-align: left;
		border: 1px solid black;
      }
    </style>
	<script type="text/javascript">
      google.load('visualization', '1', { packages: ['table'] });

      function drawTable() {
        // Construct query
        var query = "SELECT 'Type of crime', 'Shell Company Name', 'State' FROM 1DFAnYbfnDXzIYgKMDsBdX2otLEpO21kgB-na07b5";
        var crime = document.getElementById('crime').value;
        if (crime) {
          query += " WHERE 'Type of crime' = '" + crime + "'";
        }
        var queryText = encodeURIComponent(query);
        var gvizQuery = new google.visualization.Query(
            'http://www.google.com/fusiontables/v1/query?sql='  + queryText);

        // Send query and draw table with data in response
	  gvizQuery.send(function(response) {
	            var table = new google.visualization.Table(
	                document.getElementById('visualization'));
	            table.draw(response.getDataTable(), {
	              showRowNumber: true
	            });
	          });
	        }
      google.setOnLoadCallback(drawTable);
    </script>
  </head>
  <body>
    <div>
      <label>Type of crime:</label>
      <select id="crime" onchange="drawTable();">
        <option value="" selected="selected">All</option>
        <option value="Money laundering for smuggling">Money laundering for smuggling</option>
        <option value="Medicare fraud">Medicare fraud</option>
        <option value="Defrauding government to obtain contracts">Defrauding government to obtain contracts</option>
      </select>
    </div>
    <div id="visualization"></div>
  </body>
</html>