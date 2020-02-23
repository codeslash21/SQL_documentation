# SQL_documentation

### Keys:
  Primary Key (PK) : 
    A primary key is a unique column in a particular table. This is the first column in each of our tables. Here, those columns
    are all called id, but that doesn't necessarily have to be the name. It is common that the primary key is the first column in our         tables in most databases. There may be more than one primary key that is called `composite primary key` but its a bad practice.

  Foreign Key (FK):
    A foreign key is a column in one table that is a primary key in a different table. Foreign keys are always associated with a primary       key, and they are associated with the crow-foot notation above to show they can appear multiple times in a particular table. A table can has more than one foreign key.
    
### Join:
Notice our SQL query has the two tables we would like to join - one in the FROM and the other in the JOIN. Then in the ON, we will ALWAYs have the PK equal to the FK. If we wanted to join all three of these tables, we could use the same logic. The code below pulls all of the data from all of the joined tables.
`SELECT *
FROM web_events
JOIN accounts
ON web_events.account_id = accounts.id
JOIN orders
ON accounts.id = orders.account_id`
It might be nice if SQL enforced JOINs to be PK = FK, but if you want to join company name to the last name of another column, SQL will let you do it!
#### JOIN - 
An INNER JOIN that only pulls data that exists in both tables.
#### LEFT JOIN - 
Pulls all the data that exists in both tables, as well as all of the rows from the table in the FROM even if they do not exist in the JOIN statement.
#### RIGHT JOIN - 
Pulls all the data that exists in both tables, as well as all of the rows from the table in the JOIN even if they do not exist in the FROM statement
#### Outer Join:
The last type of join is a full outer join. This will return the inner join result set, as well as any unmatched rows from either of the two tables being joined.

### Aliases:
You learned that you can alias tables and columns using AS or not using it. This allows you to be more efficient in the number of characters you need to write, while at the same time you can assure that your column headings are informative of the data in your table.
`Select t1.column1 aliasname, t2.column2 aliasname2
FROM tablename AS t1
JOIN tablename2 AS t2`

### Why not Many-Many relationship:
Think about a simple relationship like the one between Authors and Books. An author can write many books. A book could have many authors. Now, without a bridge table to resolve the many-to-many relationship, what would the alternative be? You'd have to add multiple Author_ID columns to the Books table, one for each author. But how many do you add? 2? 3? 10? However many you choose, you'll probably end up with a lot of sparse rows where many of the Author_ID values are NULL and there's a good chance that you'll run across a case where you need "just one more." So then you're either constantly modifying the schema to try to accommodate or you're imposing some artificial restriction ("no book can have more than 3 authors") to force things to fit.
