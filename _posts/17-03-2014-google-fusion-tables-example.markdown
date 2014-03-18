<html>
<head>
<meta charset="UTF-8">
    <title>Fusion Tables Layer Example: Basic JSONP Request</title>
    <style type="text/css">
    #map-canvas {
           height: 500px;
           width: 600px;
         }
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
        var query = "SELECT 'Shell Company Name', 'Type of crime', 'State' FROM " + '1DFAnYbfnDXzIYgKMDsBdX2otLEpO21kgB-na07b5';
        var encodedQuery = encodeURIComponent(query);
        // Construct the URL
        var url = ['https://www.googleapis.com/fusiontables/v1/query'];
        url.push('?sql=' + encodedQuery);
        url.push('&key=AIzaSyA7UgPibV993XJ03s_nj3118ARrHHShVSI');
        url.push('&jsoncallback=?');
		console.log(url);
        // Send the JSONP request using jQuery
        $.ajax({
          url: url.join(""),
          dataType: 'jsonp',
          success: function (data) {
            var rows = data['rows'];
            var ftData = $('#ft-data');
            for (var i in rows) {
              var company = rows[i][0];
              var crime = rows[i][1];
              var state = rows[i][2];
              var html=["<div>"]
              html.append("<p class='company'>")
              html.append(company)
              html.append("</p>")
              html.append("<p class='crime'>")
              html.append(crime)
              html.append("</p><p class='state'>")
              html.append(state)
              html.append("</p></div>")
              ftData.append("".join(html));
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
