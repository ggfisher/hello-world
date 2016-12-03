##ACID - Related to the properties of Transactions   
__A__ stands for Atomicity  
__C__ stands for Consistency  
__I__ stands for Isolation  
__D__ stands for Durability  
  
__Atomicity__ - this means states that either all operations of a transaction occur on none of the operations occur.  This property is maintained by the Transaction Management Component of the database.  
  
__Consistency__ - consistency refers to __*correctness*__.  Any transaction should lead from one consistent state to another consistent state.  
  
__Isolation__ - ensures that concurrent execution results in a system state that would be obtained if a transaction had been executed serially.  This property is managed by the Concurrency Control Manager.  
  
__Durability__ - this property states that changes made by a transaction must be permanent.  The changes must __NOT__ be due to a database failure.  This property is the responsibility of the Recovery Manager.  
  
## General Definitions of Second and Third Normal Forms

### _General Definitions of Second Normal Forms_

__Definition__  A relation schema R is in second normal form (2NF) if every nonprime attribute A in R is not partially dependent on any key of R.  
  
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
- __FD5__ Area → County_name__  
  
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
  
##Boyce-Codd Normal Form

__Definition__ A relation schema R is in BCNF if whenever a nontrivial functional dependency X→A holds in R, then X is a superkey of R.

BCNF was proposed as a simpler form of 3NF, but it was found to be stricter than 3NF. That is, every relation in BCNF is also in 3NF; however, a relation in 3NF is not necessarilyin BCNF. Intuitively, we can see the need for a stronger normal form than 3NF by going back to the LOTS relation schema shown above with its four functional dependencies FD1 through FD4.  
  
If we add this to the other dependencies, the relation schema LOTS1A still is in 3NF because County_name is a prime attribute.  
  
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


  



