__*Find the names of sailors who have reserved a red or a green boat*__  

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S.sname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Sailors S, Reserves R, Boats B  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S.sid = R.sid AND R.bid = B.bid  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;AND (B.color = 'red' OR B.color = 'green') 

The previous expression can also be written as an INTERSECT operation  

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S.sname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Sailors S, Reserves R, Boats B  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S.sid = R.sid AND R.bid = B.bid  AND B.color = 'red'  
INTERSECT  
SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S2.sname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Sailors S2, Reserves R2, Boats B2  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S2.sid = R2.sid AND R2.bid = B2.bid  AND B2.color = 'green'  

This query actually contains a subtle bug if there are two sailors such as Horatio in our example instances, one of whom has reserved a red boat and the other has reserved a green boat.  In this case, the name Horatio is returned even though no one individual called Horatio has reserved both a red and a green boat. Thus, the query actually computes sailor names such that some sailor with this name has reserved a red boat and some sailor with the same name (perhaps a different sailor) has reserved a green boat.  
As we observed in Chapter 4, the problem arises because we are using sname to identify sailors, and sname is not a key for Sailors! If we select sid instead of sname in the previous query, we would compute the set of sids of sailors who have reserved both red and green boats.  

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

##Set Difference in SQL  

__*Find the sids of all sailor's who have reserved red boats but not green boats.*__  

SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S.sname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Sailors S, Reserves R, Boats B  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S.sid = R.sid AND R.bid = B.bid  AND B.color = 'red'   
UNION  
SQL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SELECT S2.sname  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FROM Sailors S2, Reserves R2, Boats B2  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WHERE S2.sid = R2.sid AND R2.bid = B2.bid  AND B2.color = 'green'  

