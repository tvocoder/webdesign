## LOOP Statement
``` sql
x := 1;
ourLoop;

LOOP
    x := x + 1;
    IF (x > 3) THEN
          EXIT ourLoop;
    END IF;
END LOOP ourLoop;
```
