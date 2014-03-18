---
layout: post
title:  "Fusion Table Test"
date:   2014-03-17 23:30:00
---

<html>
  <head>
    <meta charset="UTF-8">
    <title>Fusion Tables Layer Example: Basic JSONP Request</title>
    <style type="text/css">

      .company {
        font-weight: bold;
        margin: 10px 0px 0px 0px;
        padding: 0px;
      }

      .crime, .state {
        margin: 0px;
        padding: 0px;
      }
    </style>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js">
    </script>
    <script type="text/javascript">
      function initialize() {
        var query = "SELECT 'Shell Company Name', 'Type of crime', 'State' FROM " +
            '1DFAnYbfnDXzIYgKMDsBdX2otLEpO21kgB-na07b5';
        var encodedQuery = encodeURIComponent(query);

        // Construct the URL
        var url = ['https://www.googleapis.com/fusiontables/v1/query'];
        url.push('?sql=' + encodedQuery);
        url.push('&key=AIzaSyB4LBj2wVAP7391ptIShgpXw7vlgI30SWE');
        // url.push('&callback=?');

        // Send the JSONP request using jQuery
        $.ajax({
          url: url.join(''),
          dataType: 'jsonp',
          success: function (data) {
            var rows = data['rows'];
            var ftData = document.getElementById('ft-data');
            for (var i in rows) {
              var company = rows[i][0];
              var crime = rows[i][1];
              var state = rows[i][2];
              var dataElement = document.createElement('div');
              var companyElement = document.createElement('p');
              companyElement.innerHTML = company;
              companyElement.className = 'company';
              var crimeElement = document.createElement('p');
              crimeElement.innerHTML = crime;
              crimeElement.className = 'crime';
              var stateElement = document.createElement('p');
              stateElement.innerHTML = 'state ' + state;
              stateElement.className = 'state';

              dataElement.appendChild(companyElement);
              dataElement.appendChild(crimeElement);
              dataElement.appendChild(stateElement);
              ftData.appendChild(dataElement);
            }
          }
        });
      }
    </script>
  </head>
  <body onload="initialize()">
    <div id="ft-data"></div>
  </body>
</html>