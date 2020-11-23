## Exceptions in PL/SQL
<ul>
  <li>Exception
    <ul>
      <li>Identifier in PL/SQL</li>
      <li>Raised during the execution of a block</li>
      <li>Terminates block's main body of actions</li>
    </ul>
  </li>
  <li>Exception handlers
    <ul>
      <li>Separate routines that handle raised exceptions</li>
    </ul>
  </li>
  <li>User-defined exception
    <ul>
      <li>Defined in the declarative part of a PL/SQL block</li>
    </ul>
  </li>
</ul>

``` pgsql
DECLARE
  vpCount NUMBER;
  vStaffNo PropertyForRent.staffNo%TYPE := 'SG14';
-- define an exception for the enterprise constraint that prevents a member of staff
-- managing more than 100 properties
  
  e_too_many_properties EXCEPTION;
  PRAGMA EXCEPTION_INIT(e_too_many_properties, -20000);
  
BEGIN
     SELECT COUNT(*) INTO vpCount
     FROM PropertyForRent
     WHERE staffNo = vStaffNo;
     IF vpCount = 100
 -- raise an exception for the general constraint
        RAISE e_too_many_properties;
     END IF;
     UPDATE PropertyForRent SET staffNo = vStaffNo WHERE propertyNo = 'PG4';

EXCEPTION
-- handle the exception for the general constraint
  WHEN e_too_many_properties THEN
        dbms_output.put_lines('Member of staff' || staffNo || 'already managing 100 properties');

END;
```

## Condition Handling
<ul>
  <li>Define a handler by
    <ul>
      <li>Specifying its type</li>
      <li>Exception and completion conditions it can
      </br>resolve</li>
      <li>Action it takes to do so</li>
    </ul>
  </li>
  <li>Handler is activated
    <ul>
      <li>When it is the most appropriate handler for the
      </br>condition that has been raised by the SQL
      </br>statement</li>
    </ul></li>
  </li>
</ul>

## Cursors in PL/SQL
<ul>
  <li>Cursor
    <ul>
      <li>Allows the rows of a query result to be
      </br>accessed one at a time</li>
      <li>Must be declared and opened before use</li>
      <li>Must be closed to deactivate it after it is no
      </br>longer required</li>
      <li>Updating rows through a cursor</li>
    </ul>
  </li>
</ul>

## Using Cursors in PL/SQL to Process a Multirow Query
``` pgsql
DECLARE
      vPropertyNo   PropertyForRent.propertyNo%TYPE;
      vStreet       PropertyForRent.street%TYPE;
      vCity         PropertyForRent.city%TYPE;
      vPostcode     PropertyForRent.postcode%TYPE;
      
      CURSOR propertyCursor IS
              SELECT propertyNo, street, city, postcode
              FROM PropertyForRent
              WHERE staffNo = 'SG14'
              ORDER by propertyNo;
          
BEGIN
-- Open the cursor to start of selection, then loop to fetch each row of the result table
    OPEN propertyCursor;
    LOOP
    
-- Fetch next row of the result table
      FETCH propertyCursor
            INTO vPropertyNo, vStreet, vCity, vPostcode;
      EXIT WHEN propertyCursor%NOTFOUND;
    
-- Display data
      dbms_output.put_line('Property number:' || vPropertyNo);
      dbms_output.put_line('Street:     ' || vStreet);
      dbms_output.put_line('City:     ' || vCity);
    
    IF postcode IS NOT NULL THEN
        dbms_output.put_line('Post Code:     ' || vPostCode);
    ELSE
        dbms_output.put_line('Post Code:      NULL');
    END IF;
    END LOOP;
    
    IF propertyCursor%ISOPEN THEN CLOSE propertyCursor END IF;
    
-- Error condition - print out error
EXCEPTION
    WHEN OTHERS THEN
        dbms_output.put_line('Error detected');
        IF propertyCursor%ISOPEN THEN CLOSE propertyCursor; 
        END IF;
 END;
        
```

## Cursor Flags
<ul>
  <li>%FOUND: true if the most recent fetch returns a
  </br>row</li>
  <li>%NOTFOUND: true if the most recent fetch
  </br>returns no row</li>
  <li>%ISOPEN: true if cursor is open</li>
  <li>%ROWCOUNT: total number of rows returned so
  </br>far</li>
</ul>

