
<html>
  <head>
    <!--Load the AJAX API-->
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">


      google.charts.load('current', {'packages':['corechart']});


      google.charts.setOnLoadCallback(initialize);

      function initialize() {
        var opts = {sendMethod: 'auto'};
        var queryString = encodeURIComponent('SELECT C, H');

        var query = new google.visualization.Query(
        'https://docs.google.com/spreadsheets/d/1Of1qzPE-9AjRG9tH8-_IgDMr572Jhl9EaXUIKElUugU/gviz/tq?gid=483614174&headers=1&tq=' + queryString);


        query.send(handleQueryResponse);
      }

      function handleQueryResponse(response) {
        if (response.isError()) {
          alert('Error in query: ' + response.getMessage() + ' ' + response.getDetailedMessage());
          return;
        }

        var data = response.getDataTable();

        var options = {
          title: 'Company Performance'
        };

        var chart = new google.visualization.ScatterChart(document.getElementById('chart_div'));
        chart.draw(data, options);
      }
    </script>
  </head>

  <body>
    <div id="chart_div"></div>
  </body>
</html>
