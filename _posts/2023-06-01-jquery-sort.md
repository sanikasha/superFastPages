---
title: JQuery Sort
comments: true
layout: base
description: Try simple table with JQuery Sort
permalink: /frontend/jquery
tags: [javascript]
---
<head>
    <!-- JQuery -->
    <script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-3.5.1.js"></script>
    <script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.13.4/js/jquery.dataTables.min.js"></script>
    <!-- Bootstrap -->
    <script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.13.4/js/dataTables.bootstrap5.min.js"></script>
    <style>
        #flaskTable th:first-child {
            width: 75px;
        }
        #flaskTable td:not(:first-child) {
          width: 150px;
        }
    </style>
    <button id="insertionSortBtn" class="btn btn-primary">Sort</button>
</head>

<table id="flaskTable" class="table table-striped nowrap" style="width:100%">
    <thead id="flaskHead">
        <tr>
            <th>acous</th>
            <th>artist</th>
            <th>bpm</th>
            <th>dance</th>
            <th>duration</th>
            <th>energy</th>
            <th>id</th>
            <th>live</th>
            <th>loud</th>
            <th>popular</th>
            <th>speech</th>
            <th>title</th>
            <th>genre</th>
            <th>valence</th>
            <th>year</th>
        </tr>
    </thead>
    <tbody id="flaskBody"></tbody>
</table>

<script>
  //  insertion sort function in JS converted from my past python version
  function insertionSort(list) {
  var n = list.length;
  for (var i = 1; i < n; i++) {
    var key = list[i];
    var j = i - 1;
    while (j >= 0 && compareValues(list[j][0], key[0]) > 0) {
      list[j + 1] = list[j];
      j = j - 1;
    }
    list[j + 1] = key;
  }
  return list;
}

// this function's purpose is to compare string values; otherwise they just show up as numbers when insertion sort is run
function compareValues(a, b) { 
  if (typeof a === 'string' && typeof b === 'string') {
    return a.localeCompare(b, 'en', { numeric: true });
  }
  return a - b;
}



  $(document).ready(function() {
    fetch('https://playourshiny.duckdns.org/songdatabase', { mode: 'cors' })
      .then(response => {
        if (!response.ok) {
          throw new Error('API response failed');
        }
        return response.json();
      })
      .then(data => {
        for (const row of data) {
          $('#flaskBody').append('<tr><td>' +
            row.acousticness + '</td><td>' +
            row.artist + '</td><td>' +
            row.bpm + '</td><td>' +
            row.danceability + '</td><td>' +
            row.duration + '</td><td>' +
            row.energy + '</td><td>' +
            row.id + '</td><td>' +
            row.liveness + '</td><td>' +
            row.loudness + '</td><td>' +
            row.popularity + '</td><td>' +
            row.speechiness + '</td><td>' +
            row.title + '</td><td>' +
            row.top_genre + '</td><td>' +
            row.valence + '</td><td>' +
            row.year + '</td></tr>');
        }

        // Insertion sort function for table
        $('#insertionSortBtn').on('click', function() {
          // Retrieve table data
          var table = $('#flaskTable').DataTable();
          var tableData = table
            .columns()
            .data()
            .toArray();

          // Convert table data to a flat array
          var flatData = tableData.reduce(function(acc, val) {
            return acc.concat(val);
          }, []);

          // Perform insertion sort on the flat data array
          var sortedData = insertionSort(flatData);

          // Update table with sorted data
          var sortedTableData = [];
          var numColumns = tableData.length;
          for (var i = 0; i < sortedData.length; i += numColumns) {
            sortedTableData.push(sortedData.slice(i, i + numColumns));
          }
          table.clear().rows.add(sortedTableData).draw();
        });

        $('#flaskTable').DataTable();
      })
      .catch(error => {
        console.error('Error:', error);
      });
  });
</script>
