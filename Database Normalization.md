
##Definitions

__Definition__. A superkey of a relation schema R = {A1, A2, ... , An} is a set of attributes S⊆R with the property that no two tuples t1 and t2 in any legal relation state r of R will have t1[S] = t2[S].A key K is a superkey with the additional property that removal of any attribute from K will cause K not to be a superkey any more.

The difference between a key and a superkey is that a key has to be minimal; that is, if we have a key K = {A1,A2,...,Ak} of R,then K – {Ai} is not a key of R for any Ai,1 ≤ i ≤ k. 

In the following schema, 

|Ename|_**SSn**_|Bdate|Address|Dnumber|
|---|---|---|---|---|

{Ssn} is a key for EMPLOYEE, whereas {Ssn}, {Ssn, Ename}, {Ssn,Ename,Bdate},and any set of attributes that includes Ssn are all superkeys. If a relation schema has more than one key, each is called a candidate key. One of the candidate keys is arbitrarily designated to be the primary key, and the others are called secondary keys. In a practical relational database, each relation schema must have a primary key. If no candidate key is known for a relation, the entire relation can be treated as a default superkey. In the previous schema, {Ssn} is the only candidate key for EMPLOYEE,so it is also the primary key. 

An attribute of relation schema R is called a __prime attribute__ of R if it is a member of some candidate key of R. An attribute 
is called __nonprime__ if it is not a prime attribute—that is, if it is not a member of any candidate key.

In the following schema, both Ssn and Pnumber are prime attributes whereas the __Hours__ attribute is nonprime:

|_**Ssn**_|_**Pnumber**_|Hours|
|---|---|---|

__Definition__. Insertion Anomalies, Deletion Anomalies, Modification Anomalies, Spurious Joins

##Functional Dependencies

A functional dependency is a constraint between two sets of attributes from the database. Suppose that our relational database schema has n attributes A1, A2, ..., An; let us think of the whole database as being described by a single universal relation schema R= {A1,A2,...,An}.  We do not imply that we will actually store the database as a single universal table; we use this concept only in developing the formal theory of data dependencies.

__Definition__. A functional dependency, denoted by X → Y, between two sets of attributes X and Y that are subsets of R specifies a constraint on the possible tuples that can form a relation state r of R. The constraint is that, for any two tuples t1 and t2 in r that have t1[X] = t2[X], they must also have t1[Y] = t2[Y]. This means that the values of the Y component of a tuple in r depend on, or are determined by, the values of the Xcomponent; alternatively, the values of the Xcomponent of a tuple uniquely (or __functionally__) determine the values of the Y component. We also say that there is a functional dependency from X to Y, or that Y is functionally dependentonX.The abbreviation for functional dependency is FD or f.d. The set of attributes X is called the __left-hand side__ of the FD, and Y is called the __right-hand side__.

Thus, X functionally determines Y in a relation schema R if, and only if, whenever two tuples of r(R) agree on their X-value, they must necessarily agree on their Y value.

Consider the following schema:

|_**Ssn**_|_**Pnumber**_|Hours|Ename|Pname|Plocation|
|---|---|---|---|---|---|

and assume that following functional dependencies should hold:

- Ssn→Ename 
- Pnumber →{Pname,Plocation} 
- {Ssn,Pnumber}→Hours

These functional dependencies specify that (a) the value of an employee’s Social Security number (Ssn) uniquely determines the employee name (Ename), (b) the value of a project’s number (Pnumber) uniquely determines the project name (Pname) and location (Plocation), and (c) a combination of Ssn and Pnumber values uniquely determines the number of hours the employee currently works on the project per week (Hours).Alternatively,we say that Ename is functionally determined by (or functionally dependent on) Ssn, or given a value of Ssn, we know the value of Ename, and so on. 

##Normalization of Relations

Normalization of data can be considered a process of analyzing the given relation schemas based on their FDs and primary keys to achieve the desirable properties of (1) minimizing redundancy and (2) minimizing the insertion, deletion, and update anomalies.

The process of normalization through decomposition must also confirm the existence of additional properties that the relational schemas, taken together, should possess. These would include two properties: 

- The nonadditive join or lossless join property, which guarantees that the spurious tuple generation problem does not occur with respect to the relation schemas created after decomposition. 

- The dependency preservation property, which ensures that each functional dependency is represented in some individual relation resulting after decomposition. 




