---
layout: page
title: running
permalink: /running/
description: Running stats and history.
nav: true
nav_order: 5
---

Following graphs show my running stats. Reported times and distances are taken from a dumb wrist watch and smart Google Maps respectively.

<div id="run-distance-time" style="width: 100%; min-height: 420px;"></div>
<div id="run-yearly-distance" style="width: 100%; min-height: 420px; margin-top: 2rem;"></div>
<div id="run-location-share" style="width: 100%; min-height: 420px; margin-top: 2rem;"></div>

<script src="https://code.highcharts.com/highcharts.js"></script>
<script src="https://code.highcharts.com/modules/data.js"></script>
<script src="https://code.highcharts.com/modules/exporting.js"></script>

<script>
  document.addEventListener("DOMContentLoaded", function () {
    const apiKey = "AIzaSyCeHh09mlbfQR4JhuG-yYTblR9O1WYj4x4";
    const sheetKey = "159ANqIowVWAfuJZRo8WvhLbNwrnVKH7MHJwDIW2-beE";

    Highcharts.chart("run-distance-time", {
      title: {
        text: "Distance covered and time taken for each run since January 2016"
      },
      data: {
        googleAPIKey: apiKey,
        googleSpreadsheetKey: sheetKey,
        googleSpreadsheetWorksheet: "Sheet1",
        startColumn: 0,
        endColumn: 2
      },
      yAxis: [
        {
          title: { text: "Distance (Km)" }
        },
        {
          title: { text: "Time (M)" },
          opposite: true
        }
      ],
      series: [
        {
          name: "Distance",
          type: "column",
          yAxis: 0,
          data: {
            googleAPIKey: apiKey,
            googleSpreadsheetKey: sheetKey,
            googleSpreadsheetWorksheet: "Sheet1",
            columns: ["Date", "Distance"]
          },
          tooltip: {
            valueSuffix: " Km"
          }
        },
        {
          name: "Time",
          type: "spline",
          yAxis: 1,
          data: {
            googleAPIKey: apiKey,
            googleSpreadsheetKey: sheetKey,
            googleSpreadsheetWorksheet: "Sheet1",
            columns: ["Date", "Time"]
          },
          tooltip: {
            valueSuffix: " M"
          }
        }
      ]
    });

    Highcharts.chart("run-yearly-distance", {
      title: {
        text: "Bar chart showing distances run year wise"
      },
      chart: {
        type: "column"
      },
      xAxis: {
        min: 2015,
        title: {
          text: "Year"
        }
      },
      yAxis: {
        min: 0,
        title: {
          text: "Distance (Km)"
        }
      },
      data: {
        googleAPIKey: apiKey,
        googleSpreadsheetRange: "Pivot Table 1",
        googleSpreadsheetKey: sheetKey,
        name: ""
      },
      legend: {
        enabled: false
      }
    });

    Highcharts.chart("run-location-share", {
      title: {
        text: "Pie chart showing percentage distance run at different places"
      },
      chart: {
        type: "pie"
      },
      data: {
        googleAPIKey: apiKey,
        googleSpreadsheetRange: "Pivot Table 2",
        googleSpreadsheetKey: sheetKey,
        name: ""
      },
      tooltip: {
        pointFormat: "{series.name}: <b>{point.percentage:.1f}%</b>"
      },
      accessibility: {
        point: {
          valueSuffix: "%"
        }
      },
      plotOptions: {
        pie: {
          allowPointSelect: true,
          cursor: "pointer",
          dataLabels: {
            enabled: true,
            format: "<b>{point.name}</b>: {point.percentage:.1f}%"
          }
        }
      }
    });
  });
</script>
