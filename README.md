<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>My Data-Driven Website</title>
<style>
  body { font-family: Arial, sans-serif; }
  table { width: 100%; border-collapse: collapse; }
  th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
  th { background-color: #f2f2f2; }
</style>
</head>
<body>
<h1>Data from Google Sheets</h1>
<table id="data-table">
  <thead>
    <tr>
      <th>Column 1</th>
      <th>Column 2</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
<script>
  fetch('https://docs.google.com/spreadsheets/d/e/2PACX-1vQakyQHSql-fgxY0GUOKvB3Z6I0rt_k7gkOjCFJxTtuI8OaGhKQ4Ib7B5H3WNE9FQ/pub?gid=602322632&single=true&output=csv')
  .then(response => response.text())
  .then(data => {
    const table = document.getElementById('data-table').getElementsByTagName('tbody')[0];
    const rows = data.split('\n');
    rows.forEach((row, index) => {
      if (index === 0) return; // skip header
      const columns = row.split(',');
      const newRow = table.insertRow(table.rows.length);
      columns.forEach(column => {
        const newCell = newRow.insertCell(-1);
        newCell.textContent = column;
      });
    });
  });
</script>
</body>
</html>
