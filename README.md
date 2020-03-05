# SQL_documentation

I think it is an important distinction to say that SQL is a language. Hence, the last word of SQL being language.

### Why SQL:
* SQL is easy to understand.
* Traditional databases allow us to access data directly.
* Traditional databases allow us to audit and replicate our data.
* SQL is a great tool for analyzing multiple tables at once.
* SQL allows you to analyze more complex questions than dashboard tools like Google Analytics.

### SQL vs. NoSQL:
You may have heard of NoSQL, which stands for not only SQL. Databases using NoSQL allow for you to write code that interacts with the data a bit differently. These NoSQL environments tend to be particularly popular for web based data, but less popular for data that lives in spreadsheets the way we have been analyzing data up to this point. One of the most popular NoSQL languages is called MongoDB.

### Why Do Businesses Choose SQL?
#### 1. Data integrity is ensured -
only the data you want entered is entered, and only certain users are able to enter data into the database.
#### 2. Data can be accessed quickly - 
SQL allows you to obtain results very quickly from the data stored in a database. Code can be optimized to quickly pull results.
#### 3. Data is easily shared - 
multiple individuals can access data stored in a database, and the data is the same for all users allowing for consistent results for anyone with access to your database.

### SQL Databases:
There are many different types of SQL databases designed for different purposes.
Some of the most popular databases include:
* MySQL
* Access
* Oracle
* Microsoft SQL Server
* Postgres

[Documentation](https://www.digitalocean.com/community/tutorials/sqlite-vs-mysql-vs-postgresql-a-comparison-of-relational-database-management-systems)

### A few key points about data stored in SQL databases:
* Data in databases is stored in tables that can be thought of just like Excel spreadsheets.
* All the data in the same column must match in terms of data type.
* Consistent column types are one of the main reasons working with databases is fast.

### Pivot Table:
A pivot table is a table of statistics that summarizes the data of a more extensive table. This summary might include sums, averages, or other statistics, which the pivot table groups together in a meaningful way. Pivot tables are a technique in data processing.

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

### NULL:
NULLs are different than a zero - they are cells where data does not exist. When identifying NULLs in a WHERE clause, we write IS NULL or IS NOT NULL. We don't use =, because NULL isn't considered a value in SQL. Rather, it is a property of the data.

There are two common ways in which you are likely to encounter NULLs:
* NULLs frequently occur when performing a LEFT or RIGHT JOIN. You saw in the last lesson - when some rows in the left table of a left join are not matched with rows in the right table, those rows will contain some NULL values in the result set.
* NULLs can also occur from simply missing data in our database.

### MAX & MIN:
Functionally, MIN and MAX are similar to COUNT in that they can be used on non-numerical columns. Depending on the column type, MIN will return the lowest number, earliest date, or non-numerical value as early in the alphabet as possible. As you might suspect, MAX does the opposite—it returns the highest number, the latest date, or the non-numerical value closest alphabetically to “Z.”

### GROUP BY:
* GROUP BY can be used to aggregate data within subsets of the data. For example, grouping for different accounts, different regions, or different sales representatives.
* Any column in the SELECT statement that is not within an aggregator must be in the GROUP BY clause.
* You can GROUP BY multiple columns at once, as we showed here. This is often useful to aggregate across a number of different segments.

### DISTINCT:
DISTINCT is always used in SELECT statements, and it provides the unique rows for all columns written in the SELECT statement. Therefore, you only use DISTINCT once in any particular SELECT statement.

### HAVING:
HAVING is the “clean” way to filter a query that has been aggregated, but this is also commonly done using a subquery. Essentially, any time you want to perform a WHERE on an element of your query that was created by an aggregate, you need to use HAVING instead.
HAVINNG apper after GROUP BY clause and before ORDER BY clause. HAVING is like WHERE, but it works on logical statements involving aggregation.

### DATE:
* DATE_TRUNC:
This allows you to truncate your date to a particular part of your date-time column. Common trunctions are day, month, and year.
* DATE_PART can be useful for pulling a specific portion of a date, but notice pulling month or day of the week (dow) means that you are no longer keeping the years in order. Rather you are grouping for certain components regardless of which year they belonged in.

### CASE:
* The CASE statement always goes in the SELECT clause.
* CASE must include the following components: WHEN, THEN, and END. ELSE is an optional component to catch cases that didn’t meet any of the other previous CASE conditions.
* You can make any conditional statement using any conditional operator (like WHERE) between WHEN and THEN. This includes stringing together multiple conditional statements using AND and OR.
* You can include multiple WHEN statements, as well as an ELSE statement again, to deal with any unaddressed conditions.

### Subquery:
`SELECT *
FROM (SELECT DATE_TRUNC('day',occurred_at) AS day,
                channel, COUNT(*) as events
      FROM web_events 
      GROUP BY 1,2
      ORDER BY 3 DESC) sub
GROUP BY day, channel, events
ORDER BY 2 DESC;`

Note that you should not include an alias when you write a subquery in a conditional statement. This is because the subquery is treated as an individual value (or set of values in the IN case) rather than as a table.
Also, notice the query here compared a single value. If we returned an entire column IN would need to be used to perform a logical argument. If we are returning an entire table, then we must use an ALIAS for the table, and perform additional logic on the entire table.

### WITH:
The WITH statement is often called a Common Table Expression or CTE. Though these expressions serve the exact same purpose as subqueries.

### LEFT, RIGHT, LENGTH:
* LEFT pulls a specified number of characters for each row in a specified column starting at the beginning (or from the left). You can pull the first three digits of a phone number using LEFT(phone_number, 3).
* RIGHT pulls a specified number of characters for each row in a specified column starting at the end (or from the right). You can pull the last eight digits of a phone number using RIGHT(phone_number, 8).
* LENGTH provides the number of characters for each row of a specified column. To get the length of each phone number as LENGTH(phone_number).
* POSITION takes a character and a column, and provides the index where that character is for each row. The index of the first position is 1 in SQL. If you come from another programming language, many begin indexing at 0. Here, you saw that you can pull the index of a comma as POSITION(',' IN city_state).
* STRPOS provides the same result as POSITION, but the syntax for achieving those results is a bit different as shown here: STRPOS(city_state, ',').

### NOTE :
* NULLs are a datatype that specifies where no data exists in SQL. They are often ignored in our aggregation functions.
* Unlike COUNT, you can only use SUM on numeric columns. However, SUM will ignore NULL values, as do the other aggregation functions.
* Notice that MIN and MAX are aggregators that again ignore NULL values.
* WHERE subsets the returnedd data based on logical statements.
* `CASE` is used to combine `WHEN` and `THEN`.
*  Both POSITION and STRPOS are case sensitive, so looking for A is different than looking for a.
* COALESCE to work with NULL values. In general, COALESCE returns the first non-NULL value passed for each row.

