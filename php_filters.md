<h1>PHP Filters</h1>
<p>Validating data = Determine if the data is in proper form.</p>
<p>Sanitizing data = Remove any illegal character from data.</p>

<div id="filter0">
  <h2>The PHP Filter Extension</h2>
  <p>PHP filters are used to validate and sanitize external input.</p>
  <p>The PHP filter extension has many of the functions needed for
    </br>checking user input, and is designed to make data validation
    </br>easier and quicker.</p>
  <p>The <b>filter_list()</b> function can be used to list what
    </br>the PHP filter extension offers:</p>
  </div>
  
<div>
  <h3>Example</h3>
</div>

``` html
<table>
  <tr>
    <td>Filter Name</td>
    <td>Filter ID</td>
  </tr>
  <?php
   for each(filter_list) as $id=>$filter) {
echo '<tr><td' . $filter . '</td><td>' . filter_id($filter) . '</td></tr>';
}
  ?>
</table>
``` 

<div>
  <h2>Why Use Filters?</h2>
  <p>Many web applications receive external input. External input/data can be:</p>
  <ul>
    <li>User input from a string</li>
    <li>Cookies</li>
    <li>Web services data</li>
    <li>Server variables</li>
    <li>Database query results</li>
  </ul>
</div>

<div>
  <h4>You should always validate external data</h4>
  <p>Invalid submitted data can lead to security problems and
    </br>break your webpage!</p>
  <p>By using PHP filters you can be sure your application gets 
    </br>the correct input!</p>
</div>

<div>
  <h2>PHP filter_var() Function</h2>
  <p>The filter_var() function both validate and sanitize data.</p>
  <p>The filter_var() function filters a single variable with a
    </br>specified filter. It takes two pieces of data:
    <ul><li>The variable you want to check</li>
  <li>The type of check to use</li>
    </ul></p>
  
