---
title: rgraph
---

<html>

<script src="RGraph.common.sheets.js"></script>
<script src="RGraph.common.key.js"></script>
<script src="RGraph.bar.js"></script>

<script>
    // Create a new RGraph Sheets object using the key of the spreadsheet and
    // the callback function that creates the chart. The RGraph.Sheets object is
    // passed to the callback function as an argument so it doesn't need to be
    // assigned to a variable when it's created
    new RGraph.Sheets('1ncvARBgXaDjzuca9i7Jyep6JTv9kms-bbIzyAxbaT0E', function (sheet)
    {
        // Get the labels from the spreadsheet by retrieving part of the first row
        var labels = sheet.get('A2:A7');
        
        // Use the column headers (ie the names) as the key
        var key = sheet.get('B1:E1');
        
        // Get the data from the sheet as the data for the chart
        var data   = [
            sheet.get('B2:E2'), // January
            sheet.get('B3:E3'), // February
            sheet.get('B4:E4'), // March
            sheet.get('B5:E5'), // April
            sheet.get('B6:E6'), // May
            sheet.get('B7:E7')  // June
        ];

        // Create and configure the chart; using the information retrieved above
        // from the spreadsheet
        var bar = new RGraph.Bar({
            id: 'cvs',
            data: data,
            options: {
                backgroundGridVlines: false,
                backgroundGridBorder: false,
                labels: labels,
                xlabelsOffset: 5,
                colors: ['#A8E6CF','#DCEDC1','#FFD3B6','#FFAAA5'],
                shadow: false,
                strokestyle: 'rgba(0,0,0,0)',
                scaleZerostart: true,
                noxaxis: true,
                gutterLeft: 50,
                gutterBottom: 70,
                key: key,
                keyBoxed: false,
                keyPosition: 'gutter',
                keyTextSize: 12,
                axisColor: '#aaa'
            }
        }).wave();
    });
</script>
</html>
