
##Definitions

__Definition__. A superkey of a relation schema R = {A1, A2, ... , An} is a set of attributes S ⊆ R with the property that no two tuples t1 and t2 in any legal relation state r of R will have t1[S] = t2[S]. A key K is a superkey with the additional property that removal of any attribute from K will cause K not to be a superkey any more.

The difference between a key and a superkey is that a key has to be minimal; that is, if we have a key K = {A1,A2,...,Ak} of R, then 
K – {Ai} is not a key of R for any Ai, 1 ≤ i ≤ k.

In the following schema: 

|Ename|_**SSn**_|Bdate|Address|Dnumber|
|---|---|---|---|---|

{Ssn} is a key for EMPLOYEE, whereas {Ssn}, {Ssn, Ename}, {Ssn,Ename,Bdate}, and any set of attributes that includes Ssn are all superkeys. If a relation schema has more than one key, each is called a candidate key. One of the candidate keys is arbitrarily designated to be the primary key, and the others are called secondary keys. In a practical relational database, each relation schema must have a primary key. If no candidate key is known for a relation, the entire relation can be treated as a default superkey. In the previous schema, {Ssn} is the only candidate key for EMPLOYEE, so it is also the primary key. 

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

Consider the following schema - with the combination of __Ssn__ and __Pnumber__ being the primary key:

|_**Ssn**_|_**Pnumber**_|Hours|Ename|Pname|Plocation|
|---|---|---|---|---|---|

and assume that the following functional dependencies hold:

- Ssn→Ename 
- Pnumber →{Pname,Plocation} 
- {Ssn,Pnumber}→Hours

These functional dependencies specify that (a) the value of an employee’s Social Security number (Ssn) uniquely determines the employee name (Ename), (b) the value of a project’s number (Pnumber) uniquely determines the project name (Pname) and location (Plocation), and (c) a combination of Ssn and Pnumber values uniquely determines the number of hours the employee currently works on the project per week (Hours). Alternatively,we say that Ename is functionally determined by (or functionally dependent on) Ssn, or given a value of Ssn, we know the value of Ename, and so on. 

##Normalization of Relations

Normalization of data can be considered a process of analyzing the given relation schemas based on their FDs and primary keys to achieve the desirable properties of (1) minimizing redundancy and (2) minimizing the insertion, deletion, and update anomalies.

The process of normalization through decomposition must also confirm the existence of additional properties that the relational schemas, taken together, should possess. These would include two properties: 

- The nonadditive join or lossless join property, which guarantees that the spurious tuple generation problem does not occur with respect to the relation schemas created after decomposition. 

- The dependency preservation property, which ensures that each functional dependency is represented in some individual relation resulting after decomposition. 

##First Normal Form

It states that the domain of an attribute must include only atomic (simple,indivisible) values and that the value of any attribute in a tuple must be a single value from the domain of that attribute.

Consider the following schema for a relation called __Department__:

|Dname|_**Dnumber**_|Dmgr_ssn|Dlocations|
|---|---|---|---|

and sample state of relation __Department__:

|Dname|_**Dnumber**_|Dmgr_ssn|Dlocations|
|---|---|---|---|
|Research|5|333445555|{Bellaire,Sugarland,Houston}|
|Administration|4|987654321|{Stafford}|
|Headquarters|1|888665555|{Houston}|

This relation is not in 1NF due to the violation of the requirement for atomic values.  There are two ways to correct this:

1.  Remove the attribute Dlocations that violates 1NF and place it in a separate relation DEPT_LOCATIONS along with the primary key Dnumber of DEPARTMENT. The primary key of this relation is the combination {Dnumber, Dlocation}, as shown:

_DEPARTMENT snapshot_

|Dname|_**Dnumber**_|Dmgr_ssn|
|---|---|---|
|Research|5|333445555|
|Administration|4|987654321|
|Headquarters|1|888665555|

_DEPT_LOCATIONS snapshot_

|_**Dnumber**_|_**Dlocations**_|
|---|---|
|1|Houston|
|4|Stafford|
|5|Bellaire|
|5|Sugarland|
|5|Houston|

A distinct tuple in DEPT_LOCATIONS exists for each location of a department.This decomposes the non-1NF relation into two 1NF relations.

2. Expand the key so that there will be a separate tuple in the original __DEPARTMENT__ relation for each location of a __DEPARTMENT__, as shown below. In this case, the primary key becomes the combination {Dnumber, Dlocation}. This solution has the disadvantage of introducing redundancy in the relation. 

__1NF of DEPARTMENT Relation__

|Dname|_**Dnumber**_|Dmgr_ssn|Dlocations|
|---|---|---|---|
|Research|5|333445555|Bellaire|
|Research|5|333445555|Sugarland|
|Research|5|333445555|Houston|
|Administration|4|987654321|Stafford|
|Headquarters|1|888665555|Houston|

##Second Normal Form

__Definition.__ A relation schema R is in 2NF if every nonprime attribute A in R is fully functionally dependent on the primary key of R. 

Second normal form (2NF) is based on the concept of full functional dependency. A functional dependency X → Y is a __full functional dependency__ if removal of any attribute A from X means that the dependency does not hold any more. A functional dependency X→Y is a __partial dependency__ if some attribute A ε X can be removed from X and the dependency still holds.  In the EMP_PROJ relation below,

_EMP_PROJ relation_

|_**Ssn**_|_**Pnumber**_|Hours|Ename|Pname|Plocation|
|---|---|---|---|---|---|

_EMP_PROJ relation functional dependencies:_

- __FD1__ {Ssn,Pnumber} → Hours
- __FD2__ Ssn → Ename 
- __FD3__ Pnumber → {Pname,Plocation} 


{Ssn, Pnumber} → Hours is a full dependency (neither Ssn → Hours nor Pnumber → Hours holds). However, the dependency {Ssn, Pnumber} → Ename is partial because Ssn → Ename holds.

The test for 2NF involves testing for functional dependencies whose left-hand side attributes are part of the primary key. If the primary key contains a single attribute, the test need not be applied at all. The EMP_PROJ relation is in 1NF but is not in 2NF. The nonprime attribute Ename violates 2NF because of FD2, as do the nonprime attributes Pname and Plocation because of FD3. The functional dependencies FD2 and FD3 make Ename, Pname, and Plocation partially dependent on the primary key {Ssn,Pnumber} of EMP_PROJ, thus violating the 2NF test.

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

##Third Normal Form

__Definition.__ According to Codd’s original definition, a relation schema R is in 3NF if it satisfies 2NF and no nonprime attribute of R is transitively dependent on the primary key.

Third normal form (3NF) is based on the concept of transitive dependency. A functional dependency X → Y in a relation schema R is a __transitive dependency__ if there exists a set of attributes Z in R that is neither a candidate key nor a subset of any key of R, and both X→Z and Z→Y hold.  The dependency Ssn → Dmgr_ssn is transitive through Dnumber in EMP_DEPT in Figure 15.3(a), because both the dependencies Ssn → Dnumber and Dnumber → Dmgr_ssn hold and Dnumber is neither a key itself nor a subset of the key of EMP_DEPT. Intuitively, we can see that the dependency of Dmgr_ssn on Dnumber is undesirable in EMP_DEPT since Dnumber is not a key of EMP_DEPT.

_EMP_DEPT relation_

|Ename|_**Ssn**_|Bdate|Address|Dnumber|Dname|Dmgr_ssn|
|---|---|---|---|---|---|---|

- __FD1__ Ssn → Ename, Bdate, Address, Dnumber
- __FD2__ Dnumber → Dname, Dmgr_ssn

The relation schema EMP_DEPT is in 2NF,since no partial dependencies on a key exist. However, EMP_DEPT is not in 3NF because of the transitive dependency of Dmgr_ssn (and also Dname) on Ssn via Dnumber. We can normalize EMP_DEPT by decomposing it into the two 3NF relation schemas ED1 and ED2 shown below:

_ED1 relation_

|Ename|_**Ssn**_|Bdate|Address|Dnumber|
|---|---|---|---|---|

_ED2 relation_

|Dnumber|Dname|Dmgr_ssn|
|---|---|---|

Intuitively, we see that ED1and ED2 represent independent entity facts about employees and departments. A NATURAL JOIN operation on ED1 and ED2 will recover the original relation EMP_DEPT without generating spurious tuples.

## General Definitions of Second and Third Normal Forms

### _General Definitions of Second Normal Forms_

__Definition__  A relation schema R is in second normal form (2NF) if every nonprime attribute A in R is not partially dependent on any key of R.

The test for 2NF involves testing for functional dependencies whose left-hand side attributes are part of the primary key. If the primary key contains a single attribute, the test need not be applied at all.

Consider the following relationship schema which describes parcels of land for sale in various counties of a state:

_LOTS relation_

|*Property_id*|_**County_name**_|_**Lot#**_|Area|Price|Tax_rate|
|---|---|---|---|---|---|

Suppose that there are two candidate keys: Property_id# and {County_name, Lot#}; that is, lot numbers are unique only within each county, but Property_id# numbers are unique across counties for the entire state.

_LOTS relation functional dependencies:_

- __FD1__ Property_id → County_name, Lot#, Area, Price, Tax_rate
- __FD2__ County_name → Property_id, Lot#, Area, Price, Tax_rate 
- __FD3__ County_name → Tax_rate
- __FD4__ Area → Price

Based on the two candidate keys Property_id# and {County_name, Lot#}, the functional dependencies FD1 and FD2 hold. Property_id is chosen as the primary key, but no special consideration will be given to this key over the other candidate key.

The dependency FD3 says that the tax rate is fixed for a given county (does not vary lot by lot within the same county), while FD4 says that the price of a lot is determined by its area regardless of which county it is in.

The LOTS relation schema violates the general definition of 2NF because Tax_rate is partially dependent on the candidate key {County_name, Lot#}, due to FD3. To normalize LOTS into 2NF, we decompose it into the two relations LOTS1 and LOTS2, as shown below:

_LOTS1 relation_

|_**Property_id**_|County_name|Lot#|Area|Price|
|---|---|---|---|---|

_LOTS2 relation_

|_**County_name**_|Tax_rate|
|---|---|

We construct LOTS1 by removing the attribute Tax_rate that violates 2NF from LOTS and placing it with County_name (the left-hand side of FD3 that causes the partial dependency) into another relation LOTS2. Both LOTS1 and LOTS2 are in 2NF. Notice that FD4 does not violate 2NF and is carried over to LOTS1.

### _General Definitions of Third Normal Forms_

__Definition__ A relation schema R is in third normal form (3NF) if, whenever a nontrivial functional dependency X → A holds in R, when either:

+ a) X is a superkey of R or
+ b) A is a prime attribute of R. 

According to this definition, LOTS2 is in 3NF. However, FD4 in LOTS1 violates 3NF because Area is not a superkey and Price is not a prime attribute in LOTS1. To normalize LOTS1 into 3NF,we decompose it into the relation schemas LOTS1A and LOTS1B as shown below:

_LOTS1A relation_

|_**Property_id**_|County_name|Lot#|Area|
|---|---|---|---|

_LOTS1B relation_

|_**Area**_|Price|
|---|---|


We construct LOTS1A by removing the attribute Price that violates 3NF from LOTS1 and placing it with Area (the lefthand side of FD4 that causes the transitive dependency) into another relation LOTS1B. Both LOTS1A and LOTS1B are in 3NF. 

Two points are worth noting about this example and the general definition of 3NF: 

- LOTS1 violates 3NF because Price is transitively dependent on each of the candidate keys of LOTS1 via the nonprime attribute Area.
- This general definition can be applied directly to test whether a relation schema is in 3NF; it does not have to go through 2NF first. If we apply the above 3NF definition to LOTS with the dependencies FD1 through FD4, we find that both FD3 and FD4 violate 3NF. Therefore, we could decompose LOTS into LOTS1A, LOTS1B, and LOTS2 directly. Hence, the transitive and partial dependencies that violate 3NF can be removed in any order.

###Interpreting the General Definition of Third Normal Form

A relation schema R __violates 3NF__ if a functional dependency X → A holds in R that does not meet either condition—meaning that it violates both conditions (a) and (b) of 3NF. This can occur due to two types of problematic functional dependencies: 

- A nonprime attribute determines another nonprime attribute. Here we typically have a transitive dependency that violates 3NF. 
- A proper subset of a key of R functionally determines a nonprime attribute. Here we have a partial dependency that violates 3NF (and also 2NF).

A relation schema R __is in 3NF__ if every nonprime attribute of R meets both of the following conditions:

- It is fully functionally dependent on every key of R. 
- It is nontransitively dependent on every key of R.

##Boyce-Codd Normal Form

__Definition__ A relation schema R is in BCNF if whenever a nontrivial functional dependency X→A holds in R, then X is a superkey of R.

BCNF was proposed as a simpler form of 3NF, but it was found to be stricter than 3NF. That is, every relation in BCNF is also in 3NF; however, a relation in 3NF is not necessarilyin BCNF. Intuitively, we can see the need for a stronger normal form than 3NF by going back to the LOTS relation schema shown above with its four functional dependencies FD1 through FD4. Suppose that we have thousands of lots in the relation but the lots are from only two counties: DeKalb and Fulton. Suppose also that lot sizes in DeKalb County are only 0.5, 0.6, 0.7, 0.8, 0.9, and 1.0 acres, whereas lot sizes in Fulton County are restricted to 1.1,1.2,...,1.9,and 2.0 acres. In such a situation we would have the additional functional dependency 

- FD5: Area → County_name. 

If we add this to the other dependencies, the relation schema LOTS1A still is in 3NF because County_name is a prime attribute.

The area of a lot that determines the county, as specified by FD5, can be represented by 16 tuples in a separate relation R(Area,County_name), LOTS1AY relation below, since there are only 16 possible Area values.  This representation reduces the redundancy of repeating the same information in the thousands of LOTS1A tuples. BCNF is a stronger normal form that would disallow LOTS1A and suggest the need for decomposing it. 

_LOTS1A relation in 3NF_

|_**Property_id**_|County_name|Lot#|Area|
|---|---|---|---|

###BCNF Normalization

_LOTS1AX relation_

|_**Property_id**_|Lot#|Area|
|---|---|---|

_LOTS1AY relation_

|_**Area**_|County_name|
|---|---|

The formal definition of BCNF differs from the definition of 3NF in that condition (b) of 3NF, which allows A to be prime, is absent from BCNF. That makes BCNF a stronger normal form compared to 3NF. In our example, FD5 violates BCNF in LOTS1A because AREA is not a superkey of LOTS1A. Note that FD5 satisfies 3NF in LOTS1A because County_name is a prime attribute (condition b), but this condition does not exist in the definition of BCNF. We can decompose LOTS1Ainto two BCNF relations LOTS1AX and LOTS1AY as shown above. This decomposition loses the functional dependency FD2 because its attributes no longer coexist in the same relation after decomposition.

In practice, most relation schemas that are in 3NF are also in BCNF. Only if X → A holds in a relation schema R with X not being a superkey and A being a prime attribute will R be in 3NF but not in BCNF. The relation schema R shown below illustrates the general case of such a relation.

|_**A**_|_**B**_|C|
|---|---|---|

- __FD1__ A,B → C
- __FD2__ C → B 


