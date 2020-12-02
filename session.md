
<cite>tutorialspoint</cite>

<div>
  <p>Cookies and Sessions are used to store information. Cookies are only stored on 
    </br>the client-side machines, while sessions get stored on
    </br>the client as well as a server.</p>
  <h3>Session</h3>
  <p>A session creates a file in a temporary directory on the server where
    </br>registered session variables and their values are stored.
    </br>This data will be available to all pages on the site during that visit.</p>
  <p>A session ends when the user closes the browser or after leaving the site,
    </br>the server will terminate the session after a predetermined period of time,
    </br>commonly 30 minutes duration.</p>
</div>

<div>
  <h3>Cookies</h3>
  <p>Cookies are text files stored on the client computer and they are kept of use 
    </br>tracking purpose. Server script sends a set of cookies to the browser.
    </br>For example name, age, or identification number etc. The browser stores
    </br>this information on a local machine for future use.</p>
  <p>When next time browser sends any request to web server then it sends those
    </br>cookies information to the server and server uses that information
    </br>to identify the user.</p>
</div>

<h2>PHP Sessions</h2>
<div>
  <p>A session is a way to store information (in variables) to be used across
    </br>multiple pages.</p>
  <p>Unlike a cookie, the information is not stored on the users computer.</p>
</div>

<div>
  <h3>What is a PHP Session?</h3>
  <p>When you work with an application, you <b>open</b> it, do some changes,
    </br>and then you <b>close</b> it. This is much like a Session. The
    </br>computer knows who you are. It knows when you start the application 
    </br>and when you end. But on the internet there is on problem:
    </br>the web server does not know who you are or what you do,
    </br>because the HTTP address doesn't maintain state.</p>
  <p>Session variables solve this problem by storing user information
    </br>to be used across multiple pages. By default, session variables
    </br>last until the user closes the browser.</p>
  <p>So; Session variables hold information about one single user, and are
    </br>available to all pages in one application.</p>
</div>

<div>
  <h3>Start a PHP Session</h3>
  <p>A session is started with the <b>session_start()</b> function.</p>
  <p>Session variables are set with the PHP global variable: <b>$_SESSION</b>.</p>
  <p>Now, let's create a new page called "demo_session1.php". In this page, we
    </br>start a new PHP session and set some session variables:</p>
</div>

<div class="note">
  <p><b>Note:</b> The <b>session_start()</b> function must be the very first thing
    </br>in your document. Before any HTML tags.</p>
</div>

<div class="example">
  <h4>Example</h4>
</div>

``` php
<?
// Start the session
session_start();
?>

<!DOCTYPE html>
<html>
<body>

<?php
// Set session variables
$_SESSION["favcolor"] = "green";
$_SESSION["favanimal"] = "cat";
echo "Session variables are set.";
?>

</body>
</html>
```

<div id="w3">
  <h2>Get PHP Session Variable Values</h2>
  <p>Next, we create another page called "demo_session2.php". From this page,
    </br>we will access the session information we set on the first page
    </br>("demo_session1.php").</p>
  <p>Notice that session variables are not passed individually to each new page,
    </br>instead they are retrieved from the session we open at the beginning
    </br>of each page(<b>session_start()</b>).</p>
  <p>Also notice that all session variable values are stored in the global
    </br><b>$_SESSION</b> variable:</p>
</div>

<div id="ex_3">
  <h4>Example</h4>
</div>

``` php
<?php
session_start();
?>

<!DOCTYPE html>
<html>
<body>

<?php
// Echo session variables that were set on previous page
echo "Favorite color is " . $_SESSION["favcolor"] . ".<br>";
echo "Favorite animal is " . $_SESSION["favanimal"] . ".";
?>

</body>
</html>
```

<div class="note"><b>Another way to show all the session variable values
  </br>for a user session is to run this code:</b></div>
  
<h4>Example</h4>

``` php
<?php
session_start();
?>

<!DOCTYPE html>
<html>
<body>

<?php
print_r($_SESSION);
?>

</body>
</html>
```

<div class="note"><h4>How does it work? How does it know it's me?</h4>
  <p>Most sessions set a user-key on the user's computer that looks something
    </br>like this: 765487cf34ert8dede5a562e4f3a7e12.
    </br>The, when a session is opened on another page,
    </br>it scans the computer for a user-key.
    </br>If there is a match, it accesses that session, if not, it starts a new session.</p>
</div>

<h2>Modify a PHP Session Variable</h2>
<p>To change a session variable, just overwrite it:</p>

<h4>Example</h4>

``` php
<?php
session_start();
?>

<!DOCTYPE html>
<html>
<body>

<?php
   // to change a session variable, just overwrite it
   $_SESSION["favcolor"] = "yellow";
   print_r($_SESSION);
?>

</body>
</html>
```
<h2>Destroy a PHP Session</h2>
<p>To remove all global session variables and destroy the session,
  </br>use <b>session_set()</b> and <b>session_destroy()</b>:</p>
  
<h3>Example</h3>

``` php
<?php
session_start();
?>

<!DOCTYPE html>
<html>
<body>

<?php
   // remove all session variables
   session_unset();
   
   // destroy the session
   session_destroy();
?>

</body>
</html>
```

<h2>Destory a PHP Session</h2>
<p>To remove all global session variables and destroy the session, 
  </br>use <b>session_unset()</b> and <b>session_destroy</b>:</p>

<h3>Example</h3>

``` php
<?php
  session_start();
?>

<!DOCTYPE html>
<html>
<body>

<?php
// remove all session variables
session_unset();

// destroy the session
session_destroy();
?>

</body>
</html>
```

