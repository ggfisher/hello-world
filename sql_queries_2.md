__*Find the names of sailors who have reserved a red or a green boat*__  

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S.sname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Sailors S, Reserves R, Boats B  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S.sid = R.sid AND R.bid = B.bid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AND (B.color = 'red' OR B.color = 'green')    

__* Find the names of sailor's who have reserved both a red and a green boat.*__  

If we were to just replace the use of OR in the previous query by AND, in analogy to the English statements of the two queries, we would retrieve the names of sailors who have reserved a boat that is both red and green. The integrity constraint that bid is a key for Boats tells us that the same boat cannot have two colors, and so the variant of the previous query with AND in place of OR will always return an empty answer set.  

The best way to handle this translation is by using a UNION operation.  

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S.sname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Sailors S, Reserves R, Boats B  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S.sid = R.sid AND R.bid = B.bid  AND B.color = 'red'   
UNION  
SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S2.sname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Sailors S2, Reserves R2, Boats B2  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S2.sid = R2.sid AND R2.bid = B2.bid  AND B2.color = 'green'  
