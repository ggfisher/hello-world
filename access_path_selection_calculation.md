###Access Path Selection Calculation

### Suppose we run select a>10 from relation ***R*** where:


|R| = 10,000 (the size of the relation in pages)  
Each Page Contains 100 bytes  
Tuples/page = 10  
Number of Directory Entries (DE)/page = 100  
The domain of **a** is an integer type with the **min** = 0 and the **max**=100  
Given this information, and assuming uniform distrubtion, what is the **selectivity** of the **σ<sub>a>10** predicate?&nbsp;&nbsp;**90%**   
How many pages then, do we expect to be output from this query?&nbsp;&nbsp;(.9 * 10,000) = 9,000  

### Assume you want to do a file scan - how much does the file scan access path cost?  In other words, how many pages, worth of units, does it take, to execute this using a file scan?  
  
10,000 pages because we have to read every page of **R** and since we are doing pipeline execution, the cost is the size of **R**.  
  
### Assume we are considering the hash index **Hash(a)** - how much does it cost for a hash index?  
  
10,000 beause a hash index is only good for equalities so again we have to scan all pages.  
  
### Assume a primary B+ Tree index on R(a).  How many page accesses will the query cost?  
It will be helpful to compute:  
  
* The **fanout** of this index, where fanout is the number of directory entries that can be stored in the page?  
  * Number of Directory Entries (DE)/page = 100  

* What is the height of this index, where the height of the index is the number of distinct levels that contain indexes for the tree?   
  * Since each Directory node has 100 children, how many levels do we need in the tree, in order to index 10,000 pages?   (100&nbsp;X&nbsp;100&nbsp;) = 10,000 so the height of the tree is **2**&nbsp;&nbsp;&nbsp;**(log<sub>100</sub>&nbsp;10,000=2)**.  

__*Note: &nbsp;Since this is a primary index, the root node of the tree, and the second level of the tree will only contain the Data Table Entries only.  The third level of the tree will contain the actual tuples that include the actual data.&nbsp;This means there are 10,000 pages at the bottom of the tree, on the third level*__  
* Final Calculation. We start be assuming that there is nothing cached in memory.  We start from the top of the tree, and we have to load pages, until we get to the left most value, and then we can start scanning.  So we start at the top of the tree, we read the Root,  we read the page on the second layer, and now we should be pointed at the start position on level three where we need to start scanning.  We know we need to read 9,000 pages to output them because all of the pages are ordered, and thus we can just read it through. So we need the following number of accesses:  
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;**log<sub>100</sub>&nbsp;10,000 + 9,000**  
  

### Assume only a secondary B+-tree on R(a) How many page accesses will the query cost? 

__*Note: &nbsp;An important distinction between a secondary index and a primary index is that the lowest layer of the tree in a secondary index does not contain the actual tuples of data as it did in the primary index.  Instead, it contains pointers to data on disk.*__  
  
It will be helpful to compute:  

* How many leaf pages do we have in a secondary index?  
  *  The answer is __**1,000**__.  

__*Note: &nbsp;The reason for this is that, whereas the Primary Index had 10,000 leaf pages and it stored the actual tuples.  For this secondary index we can store 10 times as much information in the leaf pages since we know that Data Entries are smaller than tuples by a factor of 10.  What this means is that we need a factor of 10 fewer leaf nodes to index the data on disk.  Another way of saying this, is that for the secondary index, we can store 10 times the number of data entries for each leaf page in the secondary index.*__   
  
* How many tuples are there in the relation?  
  *  10,000 pages X 10 tuples/page = __**100,000**__   
* How many leaf pages do we need to have to contain 100,000 directory entries?  
  *  We need to calculate #tuples/Date Entries per page = 100,000/100 = __**1000**__.  
  
__*Note: &nbsp;In this type of index, at the leaf node of the index, you have one directoy entry for every tuple on disk.  So in this secondary index, you only need 1000 leaf nodes in order to be able to access the 100,000 tuples on disk.__  
* What is the height of the tree?  
  *  At the leaf node, we have 1000 pages.  So how many pages above the leaf node do we need to access these 1000 pages?  We need 10 since each page of Directory Entries can hold 100 pointers - 1000/100 = 10.  And now we need the root node to be able to access these 10 pages, so there are _**3**_ levels to the Secondary Index B+ Tree.  
* __**Final Calculation.**__  In order to get to the starting page, we need to do __*2*__ accesses to get to where you need to start.  We then need to scan the number of leaf pages.  How many do we need to scan?  It is determined by taking the product of the __**selectivity**__ and the number of pages which would be __**0.9 X 1000 = 900**__.  So we have to scan 900 leaf pages, and each leaf page contains 100 pointers and each of these pointers take one page access. So we will have __**900 X 100 = 90,000**__ page accesses.   

The total number of all required accesses will then be:  
  
   __**2**__ accesses to go through the index  
   __**900**__ accesses to scan the leaf nodes  
   __**90,000**__ accesses to read the data from disk.  
  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;__**2 + 900 + 90,000**__  

### Now suppose we run select a=10 from relation ***R*** where:

Each Page Contains 100 bytes  
Tuples/page = 10  
Number of Directory Entries (DE)/page = 100  
The domain of **a** is an integer type with the **min** = 0 and the **max**=100  
Given this information, and assuming uniform distrubtion, what is the **selectivity** of the **σ<sub>a>10** predicate?&nbsp;&nbsp;**90%**

### Assume only a secondary B+-tree on R(a) How many page accesses will the query cost?  
  
__*Note: &nbsp;For a secondary B+ Tree, there are a couple of factors that we need to compute, the height of the tree, and the number of leaf pages do we have to read.__

* The height of the tree which equal to:  
   * log<sub>fanout</sub> X Number of Leaves  
   * Number of matching leaves  
   
   



