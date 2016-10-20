
## SQL queries  

Instance 83  of Sailors    

|sid|sname|rating|age|
|---|---|---|---|
|22|Dustin|7|45.0|
|29|Brutus|1|33.0|
|31|Lubber|8|55.5|
|32|Andy|8|25.5|
|58|Rusty|10|35.0|
|64|Horatio|7|35.0|
|71|Zorba|10|16.0|
|74|Horatio|9|35.0|
|85|Art|3|25.5|
|95|Bob|3|63.5|

Instance R2 of Reserves  

|sid|bid|day|
|---|---|---|
|22|101|10/10/98|
|22|102|10/10/98|
|22|103|10/8/98|
|22|104|10/7/98|
|31|102|11/10/98|
|31|103|11/6/98|
|31|104|11/12/98|
|64|101|9/5/98|
|64|102|9/8/98|
|74|103|9/8/98|

Instance HI of Boats  

|bid|bname|color|
|---|---|---|
|101|Interlake|blue|
|102|Interlake|red|
|103|Clipper|green|
|104|Marine|red|

### Some queries related to the above table  

__*Find the names of sailors who have reserved boat 103.*__

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S.sname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Sailors S  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S.sid IN (SELECT R.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Reserves R  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE R.bid = 103)

The set contains the names of the sailors associated with sid 22,31, and 74.  This query could be modified to find all sailors who have not reserved boat 103 by replacing __IN__ by __NOT IN__.  

__*Find the names of sailors 'who ha'ue reserved a red boat.*__  

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S.sname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Sailors S  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S.sid __IN__ (SELECT R.sid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Reserves R  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE R.bid =IN (SELECT B.bid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Boats B  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE B.color = 'red'))  

The result of this query would be to return the names Dustin, Lubber, and Horatio.  To find the names of sailors who have not reserved a red boat we replace the outermost __IN__ by __NOT IN__.  




