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

