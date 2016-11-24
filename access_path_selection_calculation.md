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
(**Q3b**) What is the **fanout** of this index?&nbsp;&nbsp;  
(**A3b**) **100**   
(**Q3c**) What is the height of this index?&nbsp;&nbsp;  
(**A3c**) Since each Directory node has 100 children, how many levels do we need in the tree, in order to index 10,000 pages?   (100&nbsp;X&nbsp;100&nbsp;) = 10,000 so the height of the tree is **2**&nbsp;&nbsp;&nbsp;**(log<sub>100</sub>&nbsp;10,000=2)**.  
__*Note: &nbsp;Since this is a primary index, the root node of the tree, and the second level of the tree will only contain the Data Table Entries only.  The third level of the tree will contain the actual tuples that include the actual data.&nbsp;This means there are 10,000 pages at the bottom of the tree, on the third level*__  
(**A3a**) We are assuming there is nothing cached in memory.  We start from the top of the tree, and we have to load pages, until we get to the left most value, and then we start scanning.  So we start at the top of the tree, we read the Root,  we read the page on the second layer, and now we should be pointed at the start position on level three where we need to start scanning.  We know we need to read 9,000 pages to output them because all of the pages are ordered, and thus we can just read it through. So the final calculation is:  
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**log<sub>100</sub>&nbsp;10,000 + 9,000**  
  

(**Q4**) How much does it cost to do the secondary scan?  















