
##Definitions

Definition. A superkey of a relation schema R = {A1, A2, ... , An} is a set of attributes S⊆R with the property that no two tuples t1 and t2 in any legal relation state r of R will have t1[S] = t2[S].A key K is a superkey with the additional property that removal of any attribute from K will cause K not to be a superkey any more.

An attribute of relation schema R is called a __prime attribute__ of R if it is a member of some candidate key of R. An attribute 
is called __nonprime__ if it is not a prime attribute—that is, if it is not a member of any candidate key.
