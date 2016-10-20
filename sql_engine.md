1. Compute the cross-product of the tables in the from-list - this is all of the tables in the FROM statement.
2. Delete rows in the cross-product that fail the qualification conditions - this is the WHERE clause.
3. Delete all columns that do not appear in the select-list.
4. If DISTINCT is specified, eliminate duplicate rows.
5. Sort the table according to the GROUP BY clause to identify the groups.
6. Apply the group-qualification in the HAVING clause.
7. Generate one answer row for each remaining group.

SELECT S.rating, MIN (S.age) AS minage  
FROM Sailors S  
WHERE S.age >= 18  
GROUP S.rating  
BY HAVING COUNT (*) > 1  


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
|96|Frodo|3|25.5|
