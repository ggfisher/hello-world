
>
SELECT S.name  
FROM   Sailors AS S, Reserves AS R  
WHERE  S.sid = R.sid AND R.bid = 102  

> **π<sub>name</sub>(<sub>bid=102</sub>(Sailors⋈<sub>sid</sub>Reserves))**


>  
SELECT name,age   
FROM Sailors  
WHERE age < 30  

> **π<sub>name,age</sub>(σ<sub>age<30</sub>(Sailors))**


Projection

**π<sub>name</sub>(σ<sub>bid=102</sub>(Sailors⋈<sub>sid</sub>Reserves))**

Consider the following schema:  

Suppliers(__*sid*__: integer, sname: string, address: string)   
Parts(__*pid*__: integer, pname: string, color: string)   
Catalog(__*sid: integer, pid: integer*__, cost: real)  

Find the names of suppliers who supply some red part. 

RA    **π<sub>sname</sub>(π<sub>sid</sub>((π<sub>pid</sub>σ<sub>color='red'</sub>Parts)⋈Catalog)⋈Suppliers)**

SQL          

SELECT          S.sname  
                FROM Suppliers S, Parts P, Catalog C   
                WHERE P.color=’red’ AND C.pid=P.pid AND C.sid=S.sid  
      
Find the sids of suppliers who supply some red or green part. 

RA          **π<sub>sid</sub>(π<sub>pid</sub>(σ<sub>color='red' V color='green'</sub>Parts)⋈Catalog)** 
      


