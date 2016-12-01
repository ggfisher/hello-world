## Midterm 2 Study Guide  
  
###__Important Definitions with Examples__  

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
    - Ssn → Hours  
    - Pnumber → Hours  
- However the dependency   
    - {Ssn, Pnumber} → Ename is partial because Ssn → Ename holds.  
  
If a relation schema is not in 2NF, it can be second normalized into a number of 2NF relations in which nonprime attributes are associated only with the part of the primary key on which they are fully functionally dependent. Therefore,the functional dependencies FD1, FD2, and FD3 previously shown, lead to the decomposition of EMP_PROJ into the three relation schemas EP1, EP2, and EP3 as shown below, each of which is in 2NF.  

_EP1 relation_

|_**Ssn**_|_**Pnumber**_|Hours|
|---|---|---|

_EP2 relation_

|_**Ssn**_|Ename|
|---|---|

_EP3 relation_

|_**Pnumber**_|Pname|Plocation
|---|---|---|  
  
###__Finding the Closure Set of Attributes__  
  
Being able to find the the closure of a set of attributes is an important step in finding the candidate keys of a relation.  Find the closure of (AB)<sup>+</sup> in the following relation:  

R(ABCDEF)  
  
Given the following functional dependencies:  

1) AB-->C  
2) BC-->AD  
3) D-->E  
4) CF-->B  
  
(AB)<sup>+</sup> 
- = AB&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reflexivity  
- = ABC&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Given FD 1  
- = ABCD&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Given FD 2  
- = ABCDE&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Given FD 3  
  
So (AB)<sup>+</sup> is __ABCDE__  
  
###__Irreducable Set or Canonical Form of Functional Dependencies__  
  
Used to determine if an attribute of a functional dependency is extraneous.  An attribute is said to be extranious if we can remove it without changing the closure of the set of functional dependencies.  
  
Given the following relation:  
  
R(WXYZ)  
  
And the following functional dependencies:  
  
1) X-->W  
2) WZ-->XY  
3) Y-->WXZ  

__Step 1__: Apply Decomposition Rule:  
  
This means that you perform the following decomposition:  
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&alpha;-->&beta;&gamma;  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&alpha;-->&beta;   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&alpha;-->&gamma;  
  
So we end up with the following:  
  
1) X-->W  
2) WZ-->X  
3) WZ-->Y  
4) Y-->W  
5) Y-->X  
6) Y-->Z  
  
__Step 2__: Determine if any of the FD are redundant. We do this by determing the closure of each attribute along with testing each of the FD one at a time to see if they are redundant as shown:  
  
Using FD number 1 compute (X)<sup>+</sup>  

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&alpha;(X)<sup>+</sup>=XW  

Now ignore FD number 1















###__Finding Candidate Keys__  
 
 
 
