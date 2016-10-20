
> ```
SELECT S.name  
FROM   Sailors AS S, Reserves AS R  
WHERE  S.sid = R.sid AND R.bid = 102  
```
> **π<sub>name</sub>(σ<sub>bid=102</sub>(Sailors⋈<sub>sid</sub>Reserves))**


***

> `SELECT name,age FROM Sailors WHERE age < 30`  
> **π<sub>name,age</sub>(σ<sub>age<30</sub>(Sailors))**
  
***
