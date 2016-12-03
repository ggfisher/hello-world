##Normalization Forms  
  
Normalization forms can be identified by examining the functional dependencies in conjunction with the database relations and the concept of prime verses non-prime attributes.   
   
__*Prime attribute verses non-prime attribute*__  

An attribute of relation schema R is called a __prime attribute__ of R if it is a member of some candidate key of R. An attribute 
is called __nonprime__ if it is not a prime attribute—that is, if it is not a member of any candidate key.  
  
__2NF__  
  
__Definition.__ A relation schema R is in 2NF if every nonprime attribute A in R is fully functionally dependent on the primary key of R. 

A functional dependency &alpha;-->&beta; is a __full functional dependency__ if removal of any attribute A from &alpha; means that the dependency does not hold any more. A functional dependency &alpha;-->&beta; is a __partial dependency__ if some attribute A ε &alpha; can be removed from &alpha; and the dependency still holds.  
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&alpha;-->&beta;
