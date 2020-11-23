

<div class="slide" class="objectives">
  <h2>Chapter 8- Objectives</h2>  
  <ul>
    <li>How to use the SQL programming language</li>
    <li>How to use SQL cursors</li>
    <li>How to create stored procedures</li>
    <li>How to create triggers</li>
    <li>How to use triggers to enforce integrity
    </br>constraints</li>
  </ul>
</div>

<div class="cont" class="objectives">
  <h2>Objectives (cont'd.)</h2>
  <ul>
    <li>The advantages and disadvantages of triggers</li>
    <li>How to use recursive queries</li>
  </ul>
</div>

<div class="slide" id="4">
  <h2>The SQL Programming Language</h2>
  <ul>
    <li>Impedance mismatch
      <ul>
        <li>Mixing different programming paradigms</li>
        <li>SQL is a declarative language</li>
        <li>High-level language such as C is a procedural
        </br>language</li>
        <li>SQL and 3GLs use different models to
    </br>represent data</li>
      </ul>
    </li>
  </ul>
</div>

<div class="slide" id="5">
  <h2>(cont'd.)</h2>
  <ul>
    <li>SQL/PSM (Persistent Stored Modules)</li>
    <li>PL/SQL (Procedural Language/SQL)
      <ul>
        <li>Oracle's procedural extension to SQL</li>
        <li>Two versions</li>
      </ul>
    </li>
  </ul>
</div>

<div class="slide" id="6">
  <h2>Declarations</h2>
  <ul>
    <li>Variables and constant variables must be declared
    </br>before they can be referenced</li>
    <li>Possible to declare a variable as NOT NULL</li>
    <li>%TYPE and %ROWTYPE</li>
  </ul>
</div>

<div class="slide" id="figure00">
<dl>
  <dt>[DECLARE (<i>Optional</i>)</dt>
  <dd>&#8212;&ensp;declarations]</dd>
  <dt>BEGIN (<i>Mandatory</i>)</dt> 
  <dd>&#8212;&ensp;executable statements</dd>
  <dt>[EXCEPTION</dt>
  <dd>&#8212;&ensp;exception handlers]</dd>
  <dt>END;</dt>
  </dl>
</div>                     

<div class="slide" id="8">
  <ul>
    <li>vRent NUMBER(6, 2) NOT NULL := 600;</li>
    <li>vStaffNo Staff.staffNo%TYPE;</li>
  </ul>
</div>

<div class="slide" id="9">
  <h2>Assignments</h2>
  <ul>
    <li>Variables can be assigned in three ways:
      <ul>
        <li>Using the normal assignment statement(:=)</li>
        <li>SET</li>
        <li>SQL SELECT or FETCH statement</li>
      </ul>
    </li>
  </ul>
</div>

``` sql
vX NUMBER;
....
vStaffNo := 'SG14';
vRent := 500;

SELECT COUNT(*) INTO vX
FROM PropertyForRent
WHERE staffNo = vStaffNo;
SET vStaffNo = 'SG14';
```
