<html>
  <head>
    <!--Load the AJAX API-->
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">


      google.charts.load('current', {'packages':['corechart']});


      google.charts.setOnLoadCallback(initialize);

      function initialize() {
        var opts = {sendMethod: 'auto'};
        var queryString = encodeURIComponent('SELECT C, H, L');
        var query = new google.visualization.Query(
        'https://docs.google.com/spreadsheets/d/1HL_GnURVgixzX5voqFALFy5N7-EojTb4VO4tzYk4zIo/gviz/tq?gid=1910361281&headers=1&tq=' + queryString);

        query.send(handleQueryResponse);
      }

      function handleQueryResponse(response) {
        if (response.isError()) {
          alert('Error in query: ' + response.getMessage() + ' ' + response.getDetailedMessage());
          return;
        }

        var data = response.getDataTable();
        var dataView = new google.visualization.DataView(data);
        dataView.setColumns([0,1,{sourceColumn: 2, type: "number", role: "emphasis"}]);

        var options = {
          title: 'EY 2020',
          hAxis: {title: 'Submission Date'},
          vAxis: {title: 'Days Until Verification'},
          legend: 'none'
        };

        var chart = new google.visualization.ScatterChart(document.getElementById('chart_div'));
        chart.draw(dataView, options);
      }
    </script>
  </head>

  <body>
    <p>
    This graph is populated with data from <a href="https://forms.gle/G2gBP4NVWLRrSo9A9"> this form </a>.
    </p>
    <p>
    Please do not fill out the form until your AMCAS application has been verified.
    </p>

    <div id="chart_div" style="width: 900px; height:500px;"></div>
  </body>
</html>
