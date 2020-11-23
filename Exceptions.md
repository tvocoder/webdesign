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

``` plsql
DECLARE
  vpCount NUMBER;
  vStaffNo PropertyForRent.staffNo%TYPE := 'SG14';
  -- define an exception for the enterprise constraint that prevents a member of staff
  -- managing more than 100 properties
  
  e_too_many_properties EXCEPTION;
  PRAGMA EXCEPTION_INIT(e_too_many_properties, -20000);
  
BEGIN
```
