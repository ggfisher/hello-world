###Access Path Selection Calculation

####Given the following query (select a>10 from relation ***R***):

σ<sub>a>10 - R

|R| = 10,000 (the size of the relation in pages)  
Each Page Contains 100 bytes  
Tuples/page = 10  
Number of Directory Entries (DE)/page = 100  
The domain of **a** is an integer type with the **min** = 0 and the **max**=100  
Given this information, and assuming uniform distrubtion, what is the **selectivity** of the **σ<sub>a>10** predicate?&nbsp;&nbsp;**90%**   
How many pages then, do we expect to be output from this query?&nbsp;&nbsp;(.9 * 10,000) = 9,000  



Assume we have the following indexes:  

B+ Tree(a)&nbsp;&nbsp;Secondary Index&nbsp;&nbsp;&nbsp;&nbsp; Hash(a)&nbsp;&nbsp;&nbsp;&nbsp; B+ Tree(a)&nbsp;&nbsp;Primary Index  

(**Q1**) Assume you want to do a file scan - how much does the file scan access path cost?  In other words, how many pages, worth of units, does it take, to execute this using a file scan?  
(**A1**) 10,000 pages because we have to read every page of **R** and since we are doing pipeline execution, the cost is the size of **R**.  
  
(**Q2**) Now assume we are considering the hash index **Hash(a)** - how much does it cost for a hash index?  
(**A2**) 10,000 beause a hash index is only good for equalities so we have to scan anyway.  

(**Q3a**) What is the cost to use the B+ Tree Primary Index?  
(**Q3b**) What is the **fanout** of this index?&nbsp;&nbsp;**100**
(**Q3c**) What is the height of this index?&nbsp;&nbsp;
(**A3c**) Since each Directory node has 100 children, what is the height of the tree, in order to index 10,000 pages?  (100*100*100) = 10,000 so the height of the tree is **3**.










