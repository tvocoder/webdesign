<h1>PHP MySQLi Functions</h1>
<table>
<thead>
   <tr>
   <th>Function</th>
   <th>Description</th>
   </tr>
</thead>

<div class="affected_rows">
<h1>PHP mysqli affected_rows Function</h1>
<h3>Example - Object Oriented style</h3>
<p>Return the number of affected rows from different queries:</p>
</div>

``` php
<?php
$mysql = new mysqli("localhost", "root", "", "class");

if($mysqli -> connect_errno) {
   echo "Failed to connect to MySQL: " . $mysqli -> connect_error;
   exit();
}

// Perform queries and print out affected rows
$mysqli -> query("SELECT * FROM Persons");
echo "Affected rows: " . %mysqli -> affected_rows;

$mysqli -> query("DELETE FROM Persons WHERE Age > 32");
echo "Affected rows: " . $mysqli -> affected_rwos;

$mysqli -> close();
?>
```

<h2>Usage</h2>
<p>SELECT, INSERT, UPDATE, REPLACE, or DELETE query.</p>

<h2>Syntax</h2>
<h3>Object oriented style:</h3>

``` php
$mysqli -> affected_rows
```

<h3>Procedural Style:</h3>

``` php
mysqli_affected_rows(<i>connection</i>)
```

<h4>Example - Procedural style</h4>
<p>Return the number of affected rows from different queries:</p>

``` php
<?php
  $con = mysqli_connect("localhost", "root", "", "class");
  
  if(mysqli_connect_errno()) {
    echo "Failed to connect to MySQL: " . mysqli_connect_error();
    exit();
 }
 
// Perform queries and print out affected rows
mysqli_query($con, "SELECT * FROM Persons");
echo "Affected rows: " . mysqli_affected_rows($con);

mysqli_query($con, "DELETE FROM Persons WHERE Age > 32);
echo "Affected rows: " . mysqli_affected_rows($con);

mysqli_close($con);
?>
```
