
<html>
  <head>
    <!--Load the AJAX API-->
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">

      // Load the Visualization API and the corechart package.
      google.charts.load('current', {'packages':['corechart']});

      // Set a callback to run when the Google Visualization API is loaded.
      google.charts.setOnLoadCallback(drawChart);

      // Callback that creates and populates a data table,
      // instantiates the pie chart, passes in the data and
      // draws it.
      function initialize() {
        var opts = {sendMethod: 'auto'};
        // Replace the data source URL on next line with your data source URL.
        var query = new google.visualization.Query('http://spreadsheets.google.com/tq?key=0AnD0SFr9ooPgdG83Wm&transpose=0&headers=1&merge=COLS&range=A1%3AA5%2CB1%3AC5&gid=0&pub=1', opts);         
        -
        // Optional request to return only column C and the sum of column B, grouped by C members.
        query.setQuery('select C, sum(B) group by C');

        // Send the query with a callback function.
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

        var chart = new google.visualization.LineChart(document.getElementById('chart_div'));
        chart.draw(data, options);
      }
    </script>
  </head>

  <body>
    <!--Div that will hold the pie chart-->
    <div id="chart_div"></div>
  </body>
</html>
