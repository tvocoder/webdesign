<h1>PHP JSON Functions</h1>

<h2>PHP json_decode() Function</h2>
<h3>Example</h3>
<p>Store JSON data in a PHP variable, and the decode it into a
  </br>PHP object:</p>
  
``` php
<?php
$jsonobj = '{"Peter":35, "Ben":37, "Joe":43}';

var dumb(json_decode($jsonobj));
?>
```

<h2>Definition and Usage</h2>
<p>The <b>json_decode()</b> function is used to decode or convert a
  </br>JSON object to a PHP object.</p>

<h2>Syntax</h2>
<p><code>json_decode(<i>string</i>, <i>assoc</i>, <i>depth</i>, <i>options</i>)</code><p>

<h2> Parameter Values</h2>
<table>
<thead>
   <tr>
      <th>Parameter</th>
      <th>Description</th>
    </tr>
  </thead>
  
<tr>
<td><i>string</i></td>
<td>Required. Specifies the value to be encoded</td>
</tr>

<tr>
<td><i>assoc</i></td>
<td>Optional. Specifies a boolean value. When set to true, the returned
  </br>object will be converted into an associative array. When set 
  </br>to flase, it returns an object. Default is false.</td>
</tr>

<tr>
  <td><i>depth</i></td>
  <td>Optional. Specifies the recursion depth. Default recursion
    </br>depth is 512.</td>
</tr>

<tr>
  <td><i>options</i></td>
  <td>Optional. Specifies a bitmask
    </br>(JSON_BIGINT_AS_STRING,
    </br>JSON_OBJECT_AS_ARRAY,
    </br>JSON_THROW_ON_ERROR, etc...</td>
</tr>
</table>

<h2>More Examples</h2>
<h3>Example</h3>
<p>Store JSON data in a PHP variable, and then decode it into
  </br>a PHP associative array:</p>
  
``` php
<?php
   $jsonobj = '{"Peter": 35, "Ben": 37, "Joe": 43}';
   
   var_dump(json_decode($jsonobj, true));
 ?>
```

<h3>Example</h3>
<p>How to access the values from the PHP object:</p>

``` php
<?php
   $jsonobj = '{"Peter": 35, "Ben": 37, "Joe": 43}';
   $obj = json_decode($jsonobj);
   
   echo $obj->Peter;
   echo $obj->Ben;
   echo $obj->Joe;
?>
```

<h3>Example</h3>
<p>How to access the values from the PHP associative array:</p>

``` php
<?php
  $jsonobj = '{"Peter":35, "Ben":37, "Joe":43}';
  
  $arr = json_decode($jsonobj, true);
  
  echo $arr["Peter"];
  echo $arr["Ben"];
  echo $arr["Joe"];
?>
```

<h1>PHP <code>json_encode()</code> Function</h1>
<h3>Example</h3>
<p>How to encode an associative array into a JSON object:</p>

``` php
<?php
  $age = array("Peter"=>35, "Ben"=>37, "Joe"=>43);
  
  echo json_encode($age);
?>
```

<h2>More Examples</h2>
<h3>Example</h3>
<p>How to encode an indexed array into a JSON array:</p>

``` php
<?php
  $cars = array("Volvo", "BMW", "Toyota");
  
  echo json_encode($cars);
?>
```

