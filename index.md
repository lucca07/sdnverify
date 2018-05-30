<html>
  <head>
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">
      google.charts.load('current', {'packages':['corechart']});
      google.charts.setOnLoadCallback(drawChart);

      function initialize() {
        var opts = {sendMethod: 'auto'};
        var query = new google.visualization.Query('https://docs.google.com/spreadsheets/d/1Of1qzPE-9AjRG9tH8-_IgDMr572Jhl9EaXUIKElUugU/edit#gid=483614174', opts, headers=1)

        query.setQuery('select C, E')
        query.send(handleQueryResponse);
      }
      function handleQueryResponse(response) {

        if (response.isError()) {
          alert('Error in query: ' + response.getMessage() + ' ' + response.getDetailedMessage());
          return;
        }

        var data = response.getDataTable();
        var chart = new google.visualization.ScatterChart(document.getElementById('chart_div'));
        chart.draw(data, {width: 400, height: 240});
      }
    </script>
  </head>
  <body>
    <div id="chart_div" style="width: 900px; height: 500px;"></div>
  </body>
</html>
