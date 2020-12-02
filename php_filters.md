[w3schools](w3schools.com)

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
 </div>
 
 <div>
  <h2>Sanatize a String</h2>
  <p>The following example uses the <b>filter_var()</b> function to remove all
    </br>HTML tags from a string:</p>
</div>

<div>
  <h3>Example</h3>
</div>

``` php
<?php
  $str = "<h1>Hello World!</h1>";
  $newstr = filter_var($str, FILTER_SANITIZE_STRING);
  
  echo $newstr;
?>
```

<div>
  <h2>Sanitize and Validate an Email Address</h2>
  <p>The following examples uses the <b>filter_var()</b> function to first remove
    </br>an illegal characters from the <b>$email</b> variable, then check if it
    </br>is a valid email address:</p>
 </div>

<h3>Example</h3>

``` php
<?php
$email = "john.doe@example.com";

// Remove all illegal characters from email
$email = filter_var($email, FILTER_SANITIZE_EMAIL);

// Validate e-mail
if(!filter_var($email, FILTER_VALIDATE_EMAIL) === false) {
    echo("$email is a valid email address");
    }
else {
    echo("$email is not a valid email address");
   }
?>
```

<div>
  <h2>Sanitize and Validate a URL</h2>
  <p>The following example uses the <b>filter_var()</b> function to first remove
    </br>all illegal characters from a URL, then check if <b>$url</b> is a valid URL:</p>
</div>

<div>
  <h3>Example</h3></div>
  
``` php
<?php
$url = "https://www.w3schools.com";

// Remove all illegal characters from a URL
$url = filter_var($url, FILTER_SANITIZE_URL);

// Validate URL
if(!filter_var($url, FILTER_VALIDATE_URL) === false) {
    echo("$url is a valid URL");
    }
else {
    echo("$url is not a valid URL");
  }
?>
```
