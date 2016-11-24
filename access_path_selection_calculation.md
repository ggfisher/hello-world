###Access Path Selection Calculation

####Given the following query (select a>10 from relation ***R***):

σ<sub>a>10 - R

|R| = 10,000 (the size of the relation in pages)  
Each Page Contains 100 bytes  
Tuples/page = 10  
Number of Directory Entries (DE)/page = 100  

Assume we have the following indexes:  

B+ Tree(a,b)&nbsp;&nbsp;&nbsp;&nbsp; Hash(a)&nbsp;&nbsp;&nbsp;&nbsp; B+ Tree(a)

(Q1) Assume you want to do a file scan - how much does it cost?  
(A1) 





