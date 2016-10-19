## Important Terms

###Chapter 2

***Attribute*** - a property or description of an entity. A toy department employee
entity could have attributes describing the employee’s name, salary, and years of
service.

***Domain*** - a set of possible values for an attribute.

***Entity*** - an object in the real world that is distinguishable from other objects such
as the green dragon toy.

***Relationship*** - an association among two or more entities.

***Entity set*** - a collection of similar entities such as all of the toys in the toy department.

***Relationship set*** - a collection of similar relationships

***One-to-many relationship*** - a key constraint that indicates that one entity can be
associated with many of another entity. An example of a one-to-many relationship
is when an employee can work for only one department, and a department can
have many employees.

***Many-to-many relationship*** - a key constraint that indicates that many of one
entity can be associated with many of another entity. An example of a manyto-
many relationship is employees and their hobbies: a person can have many
different hobbies, and many people can have the same hobby.

***Participation constraint*** - a participation constraint determines whether relationships
must involve certain entities. An example is if every department entity has
a manager entity. Participation constraints can either be total or partial. A total
participation constraint says that every department has a manager. A partial
participation constraint says that every employee does not have to be a manager.

***Overlap constraint*** - within an ISA hierarchy, an overlap constraint determines
whether or not two subclasses can contain the same entity.

***Covering constraint*** - within an ISA hierarchy, a covering constraint determines
where the entities in the subclasses collectively include all entities in the superclass.

***Weak entity set*** - an entity that cannot be identified uniquely without considering
some primary key attributes of another identifying owner entity. An example is
including Dependent information for employees for insurance purposes.

***Aggregation*** - a feature of the entity relationship model that allows a relationship
set to participate in another relationship set. This is indicated on an ER diagram
by drawing a dashed box around the aggregation.

###Chapter 3

***relation schema***

A relation schema can be thought of as the basic information describing
a table or relation. This includes a set of column names, the data types associated
with each column, and the name associated with the entire table. For example, a
relation schema for the relation called 

Students could be expressed using the following
representation:

Students(sid: **string**, name: **string**, login: **string**,
age: **integer**, gpa: **real**)

***relational database schema***

A relational database schema is a collection of relation schemas, describing one or more
relations.

***domain***

Domain is synonymous with data type. Attributes can be thought of as columns in a
table. Therefore, an attribute domain refers to the data type associated with a column.

***relation instance***

A relation instance is a set of tuples (also known as rows or records) that each conform
to the schema of the relation.

***relation cardinality***

The relation cardinality is the number of tuples in the relation.

***relation degree***

The relation degree is the number of fields (or columns) in the relation.

***integrity constraint***

A condition specified on a database schema and restricts the data that can be stored in an instance of the database. If a database instance satisfies all the integrity constraints specified on the database schema, it is a legal instance. A DBMS enforces integrity constraints, in that it permits only legal instances to be stored in the database.

***domain constraint***

Domain constraints in the schema specify an important condition that we want each instance of the relation to satisfy: The values that appear in a column must be drawn from the domain associated with that column. Thus, the domain of a field is essentially the type of that field, in programming language terms, and restricts the values that can appear in the field.

***Key constraint***

A key constraint is a statement that a certain minimal subset of the fields of a relation is a unique identifier for a tuple.
A set of fields that uniquely identifies a tuple according to a key constraint is called a candidate key for the relation.


***definition of a (candidate) key***

1. Two distinct tuples in a legal instance (a legal instance is an instance that satisfies all Integrity Constraints,
including the key constraint) cannot have identical values in all the fields of a key.  This means that a candidate key 
is the minimum set of attributes used to uniquely identify a tupel or record in a table.

2. No subset of the set of fields in a key is a unique identifier for a tuple.  This means that if for example, {eid} was
a candidate key, {eid,name} could not be a candidate key because {eid} is a subset of {eid,name}.

Example:

|eid|eage|ename|
|---|---|---|
|1|	20|	lisa|
|2	|20	|lisa|
|3	|30	|andy|
|2	|30	|andy|

Here, eid does not uniquely identify a tupel however, the combination of {eid,eage} does uniquely define each tuple so {eid,eage} is a candidate key.

Example:

|eid|eage|ename|
|---|---|---|
|1|	20|	tony|
|2	|20	|lisa|
|3	|30	|andy|
|2	|30	|bill|

Here, the combination of {eid,eage} and {eid,ename} are both candidate keys.

***superkey***

A ***superkey*** is acandidate key plus zero or more attributes. Every candidate key is a superkey however the reverse is not true - every superkey cannot be a candidate key.  The minimal superkey is the candidate key.

Example:

|employeeID|salary|employeename|
|---|---|---|
|1|		22,000	|ernie|
|2	|	40,000	|alice|
|3	|	22,000	|bart|
|4	|	45,000	|ernie|

In this example, empoyeeID is the only candidate key

What are all the superkey's?

- employeeID
- employeeID + salary
- employeeID + employeename
- employeeID + salary + employeename

As stated, the minimal superkey is the candidate key.  Therefore, the candidate key in this case is empoyeeID.

Note that every relation is guaranteed to have a key. Since a relation is a set of tuples, the set of all fields is always a superkey.

***primary key***

A ***primary key*** is a candidate keys which has no NULL values

|employeeID	|salary|	employeename|
|---|---|---|
|1	|	22,000	|ernie|
|2	|	40,000	|alice|
|3	|	22,000	|bart|
|4	|	45,000	|NULL|

So in this relation, employeeID is a candidate key.  Also, no values in the employeeID are null, so employeeID is also the primary key.  Although employeename is a candidate key, it contains NULL values so it cannot be a primary key.

Out of all the available candidate keys, a database designer can identify a primary key.

## Chapter 5
### SQL Topics

__I will use bold italics for primary keys in this section - I don't think Markdown supports underlines.  If someone knows how to do it please add this feature to the primary keys.__

Consider the following schema:  

Sailors(__*sid*__: integer, sname: string, rating: integer, age: real)   
Boats(__*bid*__: integer, bname: string, color: string)   
Reserves(__*sid*__: integer, __*bid*__: integer, __*day*__: date)  

Example instances of the previous tables.  

An Instance of Sailors:  

|sid|sname|rating|age|
|---|---|---|---|
|22| Dustin| 7| 45.0 |
|31 |Lubber| 8| 55.5|
|58 |Rusty |10 |35.0|

An Instance of Reserves:  

|sid|bid|day|
|---|---|---|
|22|101|10/10/96|
|58|103|11/12/96|

Question:  Find the names of sailors who have reserved boat number 103.

This can be expressed in SQL as follows:  

SELECT S.sname  
FROM Sailors S, Reserves R  
WHERE S.sid = R.sid AND R.bid = 103  

The first step is to construct the cross-product of our two instances:  

|sid|sname|rating|age|sid|bid|day|
|---|---|---|---|---|---|---|
|22| Dustin| 7| 45.0 |22|101|10/10/96|
|22| Dustin| 7| 45.0 |58|103|11/12/96|
|31 |Lubber| 8| 55.5|22|101|10/10/96|
|31 |Lubber| 8| 55.5|58|103|11/12/96|
|58 |Rusty |10 |35.0|22|101|10/10/96|
|58 |Rusty |10 |35.0|58|103|11/12/96|

The second step is to apply the qualification __S.sid__ __=__ __R.sid__ AND __R.bid__ __=__ __103__.  This step eliminates all but the last row from the instance shown above.  The last step is to eliminate unwanted columns - since only _sname_ is in the SELECT clause, we return the following:  

|sname|
|---|
|Rusty |

Consider the following schema:  

Suppliers(__*sid*__: integer, sname: string, address: string)   
Parts(__*pid*__: integer, pname: string, color: string)   
Catalog(__*sid: integer, pid: integer*__, cost: real)  
