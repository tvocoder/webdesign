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
