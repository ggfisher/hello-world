##Normalization Forms  
  
Normalization forms can be identified by examining the functional dependencies in conjunction with the database relations and the concept of prime verses non-prime attributes.   
   
__*Prime attribute verses non-prime attribute*__  

An attribute of relation schema R is called a __prime attribute__ of R if it is a member of some candidate key of R. An attribute 
is called __nonprime__ if it is not a prime attribute—that is, if it is not a member of any candidate key.  
  
__2NF__  
  
__Definition.__ A relation schema R is in 2NF if every nonprime attribute A in R is fully functionally dependent on the primary key of R. 

A functional dependency &alpha;-->&beta; is a __full functional dependency__ if removal of any attribute A from &alpha; means that the dependency does not hold any more. A functional dependency &alpha;-->&beta; is a __partial dependency__ if some attribute A ε &alpha; can be removed from &alpha; and the dependency still holds.  
  
Consider the following functional dependency:  
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&alpha;-->&beta;  
  
A partial dependency would exist if __&alpha;__ were prime, only part of a candidate key and __&beta;__ were nonprime.  Here a nonprime attribute __&beta;__ depends on a part of a candidate key. This type of relation would violate 2NF.  
  
__3NF__  
  
__Definition.__ A relation schema R is in 3NF if it satisfies 2NF and no nonprime attribute of R is transitively dependent on the primary key.  
  
Third normal form (3NF) is based on the concept of transitive dependency. A functional dependency &alpha;-->&beta; in a relation schema R is a __transitive dependency__ if there exists a set of attributes &beta; in R that is neither a candidate key nor a subset of any key of R, and both &alpha;-->&gamma; and &gamma;-->&beta; hold.  
  
Consider the following functional dependency:  
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&alpha;-->&beta;  
  
Consider the case where both __&alpha;__ and __&beta;__ were both nonprime attributes.  This is showing that a nonprime attribute is functionally dependent on another nonprime attribute.  This is a case of transitive dependency and violates 3NF.  
  

