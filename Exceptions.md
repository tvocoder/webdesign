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
