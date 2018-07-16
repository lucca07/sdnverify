
<html>
  <head>
    <!--Load the AJAX API-->
    <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
    <script type="text/javascript">


      google.charts.load('current', {'packages':['corechart']});


      google.charts.setOnLoadCallback(initialize);

      function initialize() {
        var opts = {sendMethod: 'auto'};
        var queryString = encodeURIComponent('SELECT C, H, J');

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
        var Rainbow = require('rainbowvis.js');
        var rainbow = new Rainbow();
        rainbow.setNumberRange(1, data.getNumberOfRows());
        rainbow.setSpectrum('blue', 'red');

        //alter the DataTable
        var dataView = new google.visualization.DataView(data);
        dataView.setColumns([0,1,{sourceColumn: 2, role: 'emphasis'}]};
        dataView.addColumn({'type':'string', 'role':'style'});
        for (var i=0;i<data.getNumberOfRows();i++) {
          dataView.setCell(i, 3, 'point { size:3; fill-color:'+rainbow.colorAt(i+1)+'}');
        }

        var options = {
          title: 'EY 2019',
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
    This graph is populated with data from <a href="https://goo.gl/forms/xKw5dAw5AR17Ykxs1"> this form </a>.
    </p>
    <p>
    Please do not fill out the form until your AMCAS application has been verified.
    </p>

    <div id="chart_div" style="width: 900px; height:500px;"></div>
  </body>
</html>
