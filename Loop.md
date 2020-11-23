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

## WHILE/REPEAT Statement
``` sql
myLoop:
x := 1;
WHILE(x < 4) DO
      x := x+1;
END WHILE myLoop;

myLoop:
x := 1;
REPEAT
    x := x+1;
UNTIL(x > 3)
END REPEAT myLoop;
```

## FOR Statement
``` sql
SELECT COUNT(*) INTO numberOfStaff
FROM ....

myLoop:
FOR iStaff IN 1..numberOfStaff LOOP
    ....
END LOOP myLoop;
```

