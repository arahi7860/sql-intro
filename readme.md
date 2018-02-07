# SQL

## Learning Objectives

- Contrast relational and non-relational databases
- Create, set up, and seed a PostgreSQL.
- Execute SQL commands to perform CRUD actions.


## Review Questions

<details>
<summary>What is a database and why would we use one?</summary>
<br>

> A database is a tool for storing data. It offers many advantages to storying in a text or binary file:

- **Permanence**
- **Speed**
- **Consistency**
- **Scalability**
- **Querying**

</details>

<details>
<summary>What is an ERD and why would we use one?</summary>
<br>

> An **Entity Relationship Diagram** is a tool to visualize and describe the data and relationships of our programs.

</details>

<details>
<summary>How would you represent a one to many relationship?</summary>
<br>

![one-to-many]('./images/one-to-many2.png')

</details>

<details>
<summary>What is a schema?</summary>
<br>

</details>

<details>
<summary>In what format is data in a mongoose database stored?</summary>
<br>

</details>

<!-- ### Domain Modeling & ERD

- Draw an Entity Relationship Diagram (ERD)
- Identify and diagram one-to-one, one-to-many and many-to-many relationships between data entities
- Distinguish between entities and attributes
- Discuss data normalization needs and techniques -->

### Basics of Databases, and SQL

#### Concepts

- Explain what a database is and why you would use one
- Explain how a database, a database management system (DBMS) and SQL relate to one another
- Describe a database schema and how it relates to tables, rows and columns

#### Mechanics

- Create a new PostgreSQL database
- Set up a PostgreSQL database schema with a saved SQL file
- Seed a PostgreSQL database with a saved SQL file
- Execute basic SQL commands to execute CRUD actions in a database

### Relationships in SQL / SQL JOINs

- Define what a foreign key is
- Describe how to represent a one-to-many relationship in SQL database
- Explain how to represent one-to-one and many-to-many relationships in a SQL DB
- Distinguish between keys, foreign keys, and indexes
- Describe the purpose of the JOIN
- Use JOIN to combine tables in a SELECT
- Describe what it means for a database to be normalized

## Framing

This lesson is broken down into three parts...

1. [Domain Modeling & ERDs](erd_domains.md)
2. [Basics of Databases and SQL](sql_basics.md)
3. [Relationships in SQL](sql_relationships.md)

## Sample Quiz Questions


* What is the distinctive feature of a relational database?
* How is information stored in a relational database?
* What are the different types of relations that exist in a relational database?
* How do we indicate a one-to-many relationship in a database?

## Homework: [NBA Stats](https://github.com/ga-wdi-exercises/nba_stats)

## Practice

The following two resources are a great way to gain further familiarity with SQL. We fully expect this to be a challenge. If you're struggling on the homework, watch the Code School course on SQL and try the SQL for Beginners exercises before trying to finish the homework:

- [Code School Try SQL](https://www.codeschool.com/courses/try-sql)
- [SQL for Beginners](https://www.codewars.com/collections/sql-for-beginners/): Created by WDI14 graduate and current GA instructor Mike Nabil.
- [The official PostgreSQL Documentation](https://www.postgresql.org/docs/9.3/static/index.html) is also very good, in particular:
  - [The preface](https://www.postgresql.org/docs/9.3/static/preface.html)
  - [The official tutorial](https://www.postgresql.org/docs/9.3/static/tutorial.html)
  - [The overview of SQL](https://www.postgresql.org/docs/9.3/static/sql.html)

## Additional Practice

- [Postgres Guide](http://postgresguide.com/)
- [SQL Zoo](https://sqlzoo.net/)
- [W3 Schools SQL tutorial](https://www.w3schools.com/sql/)
- [SQL Course](http://www.sqlcourse.com/)
