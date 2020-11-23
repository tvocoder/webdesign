
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
      vPropertyNo     PropertyForRent.propertyNo%TYPE;
      vStreet         PropertyForRent.street%TYPE;
      vCity
      vPostcode
      
      CURSOR propertyCursor IS
            SELECT propertyNo, street, city, postcode
            FROM PropertyForRent
            WHERE staffNo = 'SG14'
            ORDER by propertyNo;
            
BEGIN
-- Open the cursor to start of selection, then loop to fetch each row of the result table
      OPEN propertyCursor;
      LOOP
        
        FETCH propertyCursor
              INTO vPropertyNo, vStreet, vCity, vPostcode,
        EXIT WHEN propertyCursor%NOTFOUND;
        
        dbms_output.put_line('Property number:' || vPropertyNo);
        dbms_output.put_line('Street:     ' || vStreet);
        dbms_output.put_line('City:     ' || vCity);
        
        IF postcode IS NOT NULL THEN
              dbms_output.put_line('Post Code:      ' || vPostcode);
        ELSE
              dbms_output.put_line('Post Code:      NULL');
        END IF;
      END LOOP;
      
      IF propertyCursor%ISOPEN THEN CLOSE propertyCursor END IF;
      
EXCEPTION
      WHEN OTHERS THEN
            dbms_output.put_line('Error detected');
            IF propertyCursor%ISOPEN THEN CLOSE propertyCursor;
            END IF;
END;
```

## Cursor Flags
<ul>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
</ul>

## Cursor Parameter
<ul>
  <li></li>
</ul>

``` pgsql

```

<ul>
  <li></li>
</ul>

``` pgsql

```

## Update Rows through a Cursor
<ul>
  <li></li>
  <li></li>
</ul>

``` pgsql

```

