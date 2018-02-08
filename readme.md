# SQL

## Learning Objectives

- Contrast relational and non-relational databases
- Create, set up, and seed a PostgreSQL.
- Describe how to represent relationships in SQL databases
- Execute SQL commands to perform CRUD actions.
- Use JOIN to combine tables in a SELECT

## Framing

Today we are going to introduce a new paradigm for persisting data in our applications. Previously, we have used mongoDB as our database when building node applications. In fact, there are many alternatives. In this lesson we will contrast a new database management system, **PostgreSQL** a relational database, with mongoDB a non-relational database.

## Review Questions

<details>
<summary>What is a database and why would we use one?</summary>
<br>

> A database is a tool for storing data. It offers many advantages to storying in a text or binary file:

- **Permanence:** Our data is safe and won't be altered or deleted. 
- **Speed:** Databases are fast! They can be thousands of times faster than reading from a file.
- **Consistency:** Databases can enforce rules that keep data uniform.
- **Scalability:** Databases can handle lots of requests per second and many are built to scale by replicating and syncing information across multiple databases
- **Querying:** Databases make it easy to search, sort, filter, and combine data using a Query Language.

</details>

<details>
<summary>What is an ERD and why would we use one?</summary>
<br>

> An **Entity Relationship Diagram** is a tool to visualize and describe the data and relationships of our programs.

</details>

<details>
<summary>How would you represent a one to many relationship?</summary>
<br>

![one-to-many](images/one-to-many2.png)

</details>

<details>
<summary>What is a schema?</summary>
<br>

> A schema is a blueprint of how your data is organized and how your database is structured. **It introduces consistency to our data.**
>
> In mongoose schemas looked like this:
```js
const CandidateSchema = new mongoose.Schema({
  name: String,
  year: Number
})
```

</details>

<details>
<summary>In what format is data in a mongoose database stored?</summary>
<br>

> Data in a non-relational database like mongodb is stored as JSON. It looks like this:

```js
{
   "_id" : ObjectId("54c955492b7c8eb21818bd09"),
   "address" : {
      "street" : "2 Avenue",
      "zipcode" : "10075",
      "building" : "1480",
      "coord" : [ -73.9557413, 40.7720266 ],
   },
   "borough" : "Manhattan",
   "cuisine" : "Italian",
   "grades" : [
      {
         "date" : ISODate("2014-10-01T00:00:00Z"),
         "grade" : "A",
         "score" : 11
      },
      {
         "date" : ISODate("2014-01-16T00:00:00Z"),
         "grade" : "B",
         "score" : 17
      }
   ],
   "name" : "Vella",
   "restaurant_id" : "41704620"
}
```

</details>

## What is a Relational Database?

### Data is stored in tables

- tables are organized by columns and rows (imagine a spreadsheet)
- tables are named according to what they model (e.g., `artists`, `songs`)
- In the case of `artists`, each row represents one artist
- Each column is called an **attribute** or **field**, such as `id`, `title`, or `birth_year`
- users are required to create schemas before data can be stored

### Queries are made via SQL (Structured Query Language)

- SQL is a database language used specifically for relational databases
- SQL is great for reliably managing complex queries

### Data is related between tables

- we can relate rows in the `songs` table to rows in the `artists` table
- to relate data we use `keys` that are unique identifiers for each row of a table.

## Lets Talk Terminology

![SQL vs noSQL comparison](images/SQL-MongoDB-comparison.png)

**Database:** The actual set of data being stored

- We may have multiple databases for an application

**Database Language:** The language used to interact with a database

- With relational databases, we use SQL
- There isn't a standard language across noSQL databases

**Database Management System (DBMS):** The software that lets a user interact (query) the data in a database

- relational examples include PostgreSQL and MySQL
- **What DBMS did we use when building MERN apps?**

**Database CLI:** A tool offered by most DBMSs that allow users to query the database from the command line

- we will use one called `psql` for PostgreSQL
- **What was the mongoose equivalent?**

### Data Compared: Collections -> Tables

Within a mongoDB database, our data is organized in JSON objects. A collection could look like this:

```js
[
  {
    "artistName" : "Prince",
    "nationality" : "American",
    "songs" : [
      {
        "songName" : "Little Red Corvet",
        "yearReleased": 1982
      },
      {
        "songName" : "Raspberry Beret",
        "yearReleased": 1985
      }
    ]
  },
  {
    "artistName" : "Sir Elton John",
    "nationality" : "British",
    "songs" : [
      {
        "songName" : "Tiny Dancer",
        "yearReleased": 1971
      },
      {
        "songName" : "Your Song",
        "yearReleased": 1970
      }
    ]
  }
]
```

In a relational database, this data would be stored in two tables.

| artistID | artistName     | nationality |
|----------|----------------|-------------|
| 1        | Prince         | American    |
| 2        | Sir Elton John | British     |

| songID | songName          | yearReleased | artistID |
|--------|-------------------|--------------|----------|
| 1      | Tiny Dancer       | 1971         | 2        |
| 2      | Little Red Corvet | 1982         | 1        |
| 3      | Raspberry Beret   | 1985         | 1        |
| 4      | Your Song         | 1970         | 2        |

### You Do: Database Conversion

> 8 mins / 2 mins

Find a partner and think of a shared interest that can be used to demonstrate a one-to-many relationship like the example above. Find a space to whiteboard and create sample JSON data. Then create tables to represent the same data.

## Relational vs Non-Relational | PostgreSQL vs MongoDB

Non-Relational or *noSQL* databases have existed in some form for decades, however their use didn't become wide spread until recently. noSQL databases became an important alternative to relational databases in the early 2000s as companies like Facebook, Google, and Amazon's data storage needs changed and expanded. With the rise of social media and online marketplaces like eBay, the amount of data on the internet boomed. User were not only getting information from the internet, they were contributing to it. This transition stressed the capabilities of relational databases due to the volume and variability of user-generated data.

noSQL databases **historically and generally** offer more flexibility and scalability than traditional relational databases. However, they come with the cost of reduced consistency.

> **NOTE: Many of the distinctions between relational and non-relational databases are becoming blurred.** While relational and noSQL databases have fundamental differences and each have pros and cons, modern technology is bridging the gap through innovations that combat the weaknesses of each model.

### MongoDB is non-relational (noSQL)

MongoDB is document based. Meaning, data is organized in collections of related documents formatted in JSON.

#### Key Advantages

##### Usability

- Documents (i.e. objects) correspond to native data types in many programming languages
- Schema-less, documents can contain data that is variable, no need for migrations

##### High Performance

- Documents can be embedded in one another reducing the need for joins.
- Simple queries are very fast

##### High Availability

MongoDB's uses replica sets by default

- automatic failover, if data is mistakenly destroyed, it's backed up elsewhere
- data redundancy can increase speed of read requests

##### Automatic Scaling

- Sharding distributes data across a cluster of servers
- Replica sets provide low-latency high-throughput deployments

### PostgreSQL is relational (SQL)

#### Key Advantages

##### SQL

- SQL is used in most relational databases meaning interaction across different relational DBMS is very similar
- SQL is well documented and robust in its utility
- SQL allows you to create dynamic relationships between tables through joins

##### Consistency

- a lot of data is tabular already, relational databases store it in a similar form
- Schemas mean you know exactly what attributes (columns) for each database entry (row)
- Schemas can check the type of data being stored to ensure data coming in is properly formated and consistent with other entries.

##### Security

- data is centrally stored so there is no inconsistency across servers
- strict schemas protect against unwanted or malicious entries
- able to comply with ACID (atomicity, consistency, isolation, durability) properties

PostgreSQL is a relational database management system. There are many others like MySQL and SQLite. They are all queried using **SQL. In a relational database, data is stored in tables.

### So which is better?

**Sorry, there's no easy answer.** While relational and non-relational databases have some key differences on paper, popular database management systems are evolving rapidly to meet the needs of a variety of users. You can likely accomplish the same goals with either a SQL or noSQL database.

In general, noSQL databases are great for unstructured or inconsistent data. Think Facebook. Facebook is rapidly evolving and it needs a flexible way to store and modify existing data. noSQL is a good fit for medical records too! Patient data may look very different between different doctors or hospital. To compare or compile this information would be nearly impossible with a relational database with a strict schema.

Relational databases are great when secure transactions are important. Banking applications may prefer the rigidity of SQL databases to monitor account data and transactions. Relational databases are also good at managing inventories and tracking deliveries. ACID compliance ensures that a process is finished to completion or not at all. You'll never lose a package or find it in two places.

## BREAK

> 10 mins

## Exploring Postgres (15 minutes / 1:25)

We are learning in order to be able to read it. We'll look stuff up when we want to write it.

But there have been times GA grads need to use it!

![SQL](./images/screenshot_kibble.png)

Start by "spotlight searching" (`command-space`) for Postgres and launching `Postgres.app`. Once you see the elephant in your Mac menu bar, you'll know Postgres is running.

### psql commands

We'll use `psql` as our primary means of interacting with our databases. Later on we'll use Ruby or server-side Javascript to do so in our programs.

Here's a quick demo. I recommend just watching and taking notes for this part. Don't try to code along.

```sql
help -- general help
\?   -- help with psql commands
\h   -- help with SQL commands
\l   -- Lists all databases

CREATE DATABASE generalassembly; -- Don't forget the semicolon!
\l -- What changed?

\c generalassembly -- Connect to generalassembly database

\d -- Lists all tables

CREATE TABLE students (
  id SERIAL PRIMARY KEY,
  first_name VARCHAR NOT NULL,
  last_name VARCHAR NOT NULL,
  quote TEXT,
  birthday VARCHAR,
  ssn INT NOT NULL UNIQUE
); -- Here we are defining a schema. More on this in just a bit...

\d

SELECT * FROM students;

INSERT INTO students (first_name, last_name) VALUES ('Andy', 'Whitely');
-- This won't work!

INSERT INTO students (first_name, last_name, quote, birthday, ssn) VALUES ('Andy', 'Whitely', 'Two goldfish are in a tank. One says, "Know how to drive this thing?"', 'April 7', 8675309);
SELECT * FROM students;

UPDATE students SET first_name = 'Andrew' WHERE first_name = 'Andy';
SELECT * FROM students;

DELETE FROM students WHERE first_name = 'Andy';
DELETE FROM students WHERE first_name = 'Andrew';

SELECT * FROM students;

DROP TABLE students; -- "drop" means to delete an entire table or database

DROP DATABASE wdi15;

\q --quits
```

In short...

- Backslash commands (e.g. `\l` ) are commands to navigate psql. These are psql-specific.
- Everything else is SQL. The SQL is what actually interacts with the database.

> If you're curious as to where exactly your databases are being stored locally, enter `SHOW data_directory;` while in psql.

### SQL Syntax

- All statements end in a semicolon
- Whitespace doesn't matter
- Uppercasing
- Always use single quotes when typing out string values
- [Ye olde style guide](http://leshazlewood.com/software-engineering/sql-style-guide/)

## Schema (10 minutes / 1:35)

Every application's database will have one or more tables. You will recall, each table stores information about a particular model (e.g., `artists`, `songs`).

Each table has a **schema**, which defines what columns it has. For each column the schema defines...

- The column's name
- the column's data type
- Any constraints for that column

### Common Data Types

Here are some common data types for SQL databases. They are all, for the most part, things you've seen before...

- Boolean
- Integer
- Float
- Text / VARCHAR
  - VARCHAR is short, TEXT is long
- NULL
- Date
- Time

> [And many more...](http://www.postgresql.org/docs/9.3/interactive/datatype.html)

### Constraints

Constraints act as limits on the data that can go in a column.
- e.g., `NOT NULL` and `UNIQUE`

> [And many more...](http://www.postgresql.org/docs/8.1/static/ddl-constraints.html)

### Defining a Schema

Next we're going to build a schema for a database in a sample application. It can change later on if we need to add / remove tables or columns, but we'll start with something simple.

Instead of typing this into `psql`, we're going to do so by saving the schema to a `.sql` file and run it, just like we have with `.js` and `.rb` files.
## You Do: Building Our Database (15 minutes / 1:50)

> 15 minutes exercise. 5 minutes review.

Clone down and follow the instructions in the
[library SQL Exercise repo](https://github.com/ga-wdi-exercises/library_sql).

## You Do: Basic SQL Queries (20 minutes / 2:10)

Complete the queries in `basic_queries.sql` in the library_sql repo.

## Relationships in SQL / SQL JOINs

One of the key features of relational databases is that they can represent relationships between rows in different tables.

Going back to our library example, we have two tables: `books` and `authors`. Our goal now is to somehow indicate the relationship between a book and an author. In this case, that relationship indicates who wrote the book.

You can imagine that we'd like to use this information in a number of ways, such as...

- Getting the author information for a given book
- Getting all books written by a given author
- Searching for books based on attributes of the author (e.g., all books written by a Chinese author)

### One-to-Many (10 minutes / 2:20)

How might we represent this information in our database? For this example,
let's assume that each book has only one author (even though that's not always
the case in the real world).

#### Option 1 - Duplicate Info (Wrong :x:)

**authors**
- name
- nationality
- birth_year

**books**
- title
- pub_date
- author_name
- author_nationality
- author_birth_year

<details>
  <summary><strong>What's the problem here?</strong></summary>

  > Duplication, difficult to keep data in sync.

</details>

#### Option 2 - Array of IDs (Wrong :x:)

**authors**
- name
- nationality
- book_ids

**books**
- title
- pub_date

<details>
  <summary><strong>What's the problem here?</strong></summary>

  > Parsing list, can't index (for speed!)

</details>

#### Option 3 (Correct! :white_check_mark:)

**authors**
- name
- nationality

**books**
- title
- pub_date
- author_id

![one_to_many](images/one_to_many.png)

## Bonus: Joins

To `SELECT` information on two or more tables at ones, we can use a `JOIN` clause.
This will produce rows that contain information from both tables. When joining
two or more tables, we have to tell the database how to match up the rows.
(e.g. to make sure the author information is correct for each book).

This is done using the `ON` clause, which specifies which properties to match.

### Writing SQL JOINS

```sql
SELECT id FROM authors where name = 'J.K. Rowling';
SELECT * FROM books where author_id = 2;

SELECT * FROM books JOIN authors ON books.author_id = authors.id;
SELECT * FROM books JOIN authors ON books.author_id = authors.id WHERE authors.nationality = 'United States of America';
```

## You Do: Books and Authors

See advanced_queries.sql in the [library_sql](https://github.com/ga-dc/library_sql)
exercise.

## Aside: Less Common Joins

There are actually a number of ways to join multiple tables with `JOIN`, if
you're really curious, check out this article:

[A visual explanation of SQL Joins](http://blog.codinghorror.com/a-visual-explanation-of-sql-joins/)

## Bonus: Many-to-Many Relationships

We're not going to go in-depth with many-to-many relationships today, but lets go over a simple example...

Consider if we wanted to add a categories model (e.g. fiction, non-fiction,
sci-fi, romance, etc). Books can belong to many categories (i.e. a book might be
a fiction/romance, or a history/non-fiction). And a given category might have
many books.

Because of this, we can't put a book_id column on categories, nor a category_id
column on books, either way, we might have more than one value in that field
(a no-no in terms of performance).

To solution is to create an additional table, which stores just the
relationships between the two tables. Such a table is called a join table, and
contains two foreign key columns.

In our example, we might create a table called 'categorizations', and it would
have a book_id and category_id. Each row would represent a specific book's
association with a specific category.

![many_to_many](images/many_to_many.png)

## Closing/Questions (10 minutes)

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
