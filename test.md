
> ```
SELECT S.name  
FROM   Sailors AS S, Reserves AS R  
WHERE  S.sid = R.sid AND R.bid = 102  
```
> **π<sub>name</sub>(σ<sub>bid=102</sub>(Sailors⋈<sub>sid</sub>Reserves))**
