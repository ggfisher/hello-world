## Midterm 2 Study Guide  

__Important Definitions with Examples__  

__*Superkey*__  
  
Given the following EMPLOYEE relation: 

|_**SSn**_|Ename|Bdate|Address|Dnumber|
|---|---|---|---|---|  
  
where SSn is the __key__ for the relation and {Ssn}, {Ssn, Ename}, {Ssn,Ename,Bdate}, and any set of attributes that includes Ssn are all superkeys. If a relation schema has more than one key, each is called a candidate key. One of the candidate keys is arbitrarily designated to be the primary key, and the others are called secondary keys. In a practical relational database, each relation schema must have a primary key. If no candidate key is known for a relation, the entire relation can be treated as a default superkey. In the previous schema, {Ssn} is the only candidate key for EMPLOYEE, so it is also the primary key. 

__*Prime attribute verses non-prime attribute*__  

An attribute of relation schema R is called a __prime attribute__ of R if it is a member of some candidate key of R. An attribute 
is called __nonprime__ if it is not a prime attribute—that is, if it is not a member of any candidate key.  
  
Given the following schema, where the primary key for the relation is {Ssn,Pnumber}, both Ssn and Pnumber are __prime attributes__ and the __Hours__ attribute is __nonprime__:  

|_**Ssn**_|_**Pnumber**_|Hours|  
|---|---|---|  

  
__*Full Functional Dependency verses Partial Functional Dependency*__  
  
These topics deal primarily with deciding whether a relation schema is in 2NF.  Althought not covered specifically in class, they are important topics to understand for the upcoming examples.  

A relation schema R is in 2NF if every nonprime attribute A in R is fully functionally dependent on the primary key of R. 

Second normal form (2NF) is based on the concept of full functional dependency. A functional dependency X → Y is a __full functional dependency__ if removal of any attribute A from X means that the dependency does not hold any more. A functional dependency X→Y is a __partial dependency__ if some attribute A ε X can be removed from X and the dependency still holds.  In the EMP_PROJ relation below,

_EMP_PROJ_ relation  

|_**Ssn**_|_**Pnumber**_|Hours|Ename|Pname|Plocation|
|---|---|---|---|---|---|

and the _EMP_PROJ_ relation functional dependencies given below:  

- __FD1__ {Ssn,Pnumber} → Hours
- __FD2__ Ssn → Ename 
- __FD3__ Pnumber → {Pname,Plocation} 
  
We can see the following:  

- {Ssn, Pnumber} → Hours is a fully functionally dependent because neither of the following hold:   
    Ssn → Hours
    Pnumber → Hours  
- The dependency {Ssn, Pnumber} → Ename is partial because Ssn → Ename holds.  

The test for 2NF involves testing for functional dependencies whose left-hand side attributes are part of the primary key. If the primary key contains a single attribute, the test need not be applied at all. The nonprime attribute Ename violates 2NF because of FD2, as do the nonprime attributes Pname and Plocation because of FD3. The functional dependencies FD2 and FD3 make Ename, Pname, and Plocation partially dependent on the primary key {Ssn,Pnumber} of EMP_PROJ, thus violating the 2NF test.

If a relation schema is not in 2NF, it can be second normalized or 2NF normalized into a number of 2NF relations in which nonprime attributes are associated only with the part of the primary key on which they are fully functionally dependent. Therefore,the functional dependencies FD1, FD2, and FD3 previously shown, lead to the decomposition of EMP_PROJ into the three relation schemas EP1, EP2, and EP3 as shown below, each of which is in 2NF.

_EP1 relation_

|_**Ssn**_|_**Pnumber**_|Hours|
|---|---|---|

_EP2 relation_

|_**Ssn**_|Ename|
|---|---|

_EP3 relation_

|_**Pnumber**_|Pname|Plocation
|---|---|---|  

__Topics__
 - __Attribute Closure__  
 - __Finding Candidate Keys__  
 - __Minimal Cover__  
 
 
 
