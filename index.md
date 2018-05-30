<html>
  <head>
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">
      google.charts.load('current', {'packages':['corechart']});
      google.charts.setOnLoadCallback(drawChart);

      function drawGID() {
        var queryString = encodeURIComponent('SELECT C, E');

        var query = new google.visualization.Query(
            'https://docs.google.com/spreadsheets/d/1Of1qzPE-9AjRG9tH8-_IgDMr572Jhl9EaXUIKElUugU/edit#gid=483614174' + queryString);
        query.send(handleQueryResponse);
      }

      function handleQueryResponse(response) {
        if (response.isError()) {
          alert('Error in query: ' + response.getMessage() + ' ' + response.getDetailedMessage());
          return;
        }

        var data = response.getDataTable();
        var chart = new google.visualization.ScatterChart(document.getElementById('chart_div'));
        chart.draw(data, {width:500, height: 400 });
      }
      function drawChart() {
       var data = google.visualization.arrayToDataTable([
         ['Age', 'Weight'],
         [ 8,      12],
         [ 4,      5.5],
         [ 11,     14],
         [ 4,      5],
         [ 3,      3.5],
         [ 6.5,    7]
       ]);

       var options = {
         title: 'Age vs. Weight comparison',
         hAxis: {title: 'Age', minValue: 0, maxValue: 15},
         vAxis: {title: 'Weight', minValue: 0, maxValue: 15},
         legend: 'none'
       };

       var chart = new google.visualization.ScatterChart(document.getElementById('chart_div'));

       chart.draw(data, options);
     }
    </script>
  </head>
  <body>
    <div id="chart_div" style="width: 900px; height: 500px;"></div>
  </body>
</html>
