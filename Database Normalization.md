
##Definitions

Definition. A superkey of a relation schema R = {A1, A2, ... , An} is a set of attributes S⊆R with the property that no two tuples t1 and t2 in any legal relation state r of R will have t1[S] = t2[S].A key K is a superkey with the additional property that removal of any attribute from K will cause K not to be a superkey any more.

The difference between a key and a superkey is that a key has to be minimal; that is, if we have a key K = {A1,A2,...,Ak} of R,then K – {Ai} is not a key of R for any Ai,1 ≤ i ≤ k. 

In the following schema, 

|Ename|_**SSn**_|Bdate|Address|Dnumber|
|---|---|---|---|---|

{Ssn} is a key for EMPLOYEE, whereas {Ssn}, {Ssn, Ename}, {Ssn,Ename,Bdate},and any set of attributes that includes Ssn are all superkeys. If a relation schema has more than one key, each is called a candidate key. One of the candidate keys is arbitrarily designated to be the primary key,and the others are called secondary keys. In a practical relational database, each relation schema must have a primary key. If no candidate key is known for a relation, the entire relation can be treated as a default superkey. In the previous schema, {Ssn} is the only candidate key for EMPLOYEE,so it is also the primary key. 

An attribute of relation schema R is called a __prime attribute__ of R if it is a member of some candidate key of R. An attribute 
is called __nonprime__ if it is not a prime attribute—that is, if it is not a member of any candidate key.

In the following schema, both Ssn and Pnumber are prime attributes whereas the __Hours__ attribute is nonprime:

|_**Ssn**_|_**Pnumber**_|Hours|
|---|---|---|
