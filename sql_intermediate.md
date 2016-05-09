## SQL intermediate

Example:
```
SELECT name, age, salary

FROM employee

WHERE age > 40;
The above statement will select all of the values in the name, age, and salary columns from the employee table whose age is greater than 40.
```

**Note:** Remember to put a semicolon at the end of your SQL statements. The ; indicates that your SQL statment is complete and is ready to be interpreted.

**Quick note about the like comparison operator**

Example:
```
SELECT name, title, dept FROM employee WHERE title LIKE 'Pro%';
```

The above statement will select all of the rows/values in the name, title, and dept columns from the employee table whose title starts with 'Pro'. This may return job titles including Programmer or Pro-wrestler.


## Aggregate functions

Aggregate Functions

```
MIN	returns the smallest value in a given column
MAX	returns the largest value in a given column
SUM	returns the sum of the numeric values in a given column
AVG	returns the average value of a given column
COUNT	returns the total number of values in a given column
COUNT(*)	returns the number of rows in a table
```



For example:
```
SELECT AVG(salary)

FROM employee;
```

This statement will return a single result which contains the average value of everything returned in the salary column from the employee table.

Another example:
```
SELECT AVG(salary)

FROM employee

WHERE title = 'Programmer';
```

This statement will return the average salary for all employee whose title is equal to 'Programmer'

Example:

```
SELECT Count(*)

FROM employee;
```

This particular statement is slightly different from the other aggregate functions since there isn't a column supplied to the count function. This statement will return the number of rows in the employees table.



## Group By

The GROUP BY clause will gather all of the rows together that contain data in the specified column(s) and will allow aggregate functions to be performed on the one or more columns. This can best be explained by an example:

**GROUP BY clause syntax**:

```
SELECT column1,
SUM(column2)

FROM "list-of-tables"

GROUP BY "column-list";
```


Let's say you would like to retrieve a list of the highest paid salaries in each dept:

Example:
```
SELECT max(salary), dept

FROM employee

GROUP BY dept;
```

This statement will select the maximum salary for the people in each unique department. Basically, the salary for the person who makes the most in each department will be displayed. Their, salary and their department will be returned.

Here's a table:
**items_ordered**

(sample of the table)
```
items_ordered

customerid	order_date	item	quantity	price
  10330	  30-Jun-1999	Pogo stick	1	28.00
  10101	  30-Jun-1999	Raft	1	58.00
  10298	  01-Jul-1999	Skateboard	1	33.00
  10101	  01-Jul-1999	Life Vest	4	125.00
  10299	  06-Jul-1999	Parachute	1	1250.00
  10339	  27-Jul-1999	Umbrella	1	4.50
  10449	  13-Aug-1999	Unicycle	1	180.79
  10439	  14-Aug-1999	Ski Poles	2	25.50
  10101	  18-Aug-1999	Rain Coat	1	18.30
  10449	  01-Sep-1999	Snow Shoes	1	45.00
  10439	  18-Sep-1999	Tent	1	88.00
  10298	  19-Sep-1999	Lantern	2	29.00
  10410	  28-Oct-1999	Sleeping Bag	1	89.22
  10438	  01-Nov-1999	Umbrella	1	6.75
  10438	  02-Nov-1999	Pillow	1	8.50
  10298	  01-Dec-1999	Helmet	1	22.00
  10449	  15-Dec-1999	Bicycle	1	380.50
  10449	  22-Dec-1999	Canoe	1	280.00
  10101	  30-Dec-1999	Hoola Hoop	3	14.75
  10330	  01-Jan-2000	Flashlight	4	28.00
  10101	  02-Jan-2000	Lantern	1	16.00
  10299	  18-Jan-2000	Inflatable Mattress	1	38.00
  10438	  18-Jan-2000	Tent	1	79.99
  10413	  19-Jan-2000	Lawnchair	4	32.00
  10410	  30-Jan-2000	Unicycle	1	192.50
  10315	  2-Feb-2000	Compass	1	8.00
  10449	  29-Feb-2000	Flashlight	1	4.50
  10101	  08-Mar-2000	Sleeping Bag	2	88.70
  10298	  18-Mar-2000	Pocket Knife	1	22.38
  10449	  19-Mar-2000	Canoe paddle	2	40.00
  10298	  01-Apr-2000	Ear Muffs	1	12.50
  10330	  19-Apr-2000	Shovel	1	16.75
```

For example, take a look at the items_ordered table. Let's say you want to group everything of quantity 1 together, everything of quantity 2 together, everything of quantity 3 together, etc. If you would like to determine what the largest cost item is for each grouped quantity (all quantity 1's, all quantity 2's, all quantity 3's, etc.), you would enter:

```
SELECT quantity, max(price)

FROM items_ordered

GROUP BY quantity;
```

I get this:

```
1	1250.00
2	88.70
3	14.75
4	125.00
```

which is right!



## Having condition

The HAVING clause allows you to specify conditions on the rows for each group - in other words, which rows should be selected will be based on the conditions you specify. The HAVING clause should follow the GROUP BY clause if you are going to use it.

HAVING clause syntax:

```
SELECT column1,
SUM(column2)

FROM "list-of-tables"

GROUP BY "column-list"

HAVING "condition";
```

HAVING can best be described by example. Let's say you have an employee table containing the employee's name, department, salary, and age. If you would like to select the average salary for each employee in each department, you could enter:

```
SELECT dept, avg(salary)


FROM employee

GROUP BY dept;
```
But, let's say that you want to ONLY calculate & display the average if their salary is over 20000:

```
SELECT dept, avg(salary)

FROM employee

GROUP BY dept

HAVING avg(salary) > 20000;
```


## ORDER BY clause

ORDER BY is an optional clause which will allow you to display the results of your query in a sorted order (either ascending order or descending order) based on the columns that you specify to order by.


ORDER BY clause syntax:
```

SELECT column1, SUM(column2) FROM "list-of-tables" ORDER BY "column-list" [ASC | DESC];

[ ] = optional
```
This statement will select the employee_id, dept, name, age, and salary from the employee_info table where the dept equals 'Sales' and will list the results in Ascending (default) order based on their Salary.

```
SELECT employee_id, dept, name, age, salary FROM employee_info WHERE dept = 'Sales' ORDER BY salary;
```



If you would like to order based on multiple columns, you must seperate the columns with commas. For example:

```
SELECT employee_id, dept, name, age, salary


FROM employee_info

WHERE dept = 'Sales'

ORDER BY salary, age DESC;
```




## Using booleans

Combining Conditions & Boolean Operators in where clauses.

The AND operator can be used to join two or more conditions in the WHERE clause. Both sides of the AND condition must be true in order for the condition to be met and for those rows to be displayed.

```
SELECT column1,
SUM(column2)

FROM "list-of-tables"


WHERE "condition1" AND
"condition2";
```



The OR operator can be used to join two or more conditions in the WHERE clause also. However, either side of the OR operator can be true and the condition will be met - hence, the rows will be displayed. With the OR operator, either side can be true or both sides can be true.

For example:

```
SELECT employeeid, firstname, lastname, title, salary


FROM employee_info

WHERE salary >= 50000.00 AND title = 'Programmer';
```

This statement will select the employeeid, firstname, lastname, title, and salary from the employee_info table where the salary is greater than or equal to 50000.00 AND the title is equal to 'Programmer'. Both of these conditions must be true in order for the rows to be returned in the query. If either is false, then it will not be displayed.


Although they are not required, you can use paranthesis around your conditional expressions to make it easier to read:

```
SELECT employeeid, firstname, lastname, title, salary

FROM employee_info

WHERE (salary >= 45000.00) AND (title = 'Programmer');
```



### Mathematical operators

The modulo operator determines the integer remainder of the division. This operator is not ANSI SQL supported, however, most databases support it. The following are some more useful mathematical functions to be aware of since you might need them. These functions are not standard in the ANSI SQL-92 specs, therefore they may or may not be available on the specific RDBMS that you are using. However, they were available on several major database systems that I tested. They WILL work on this tutorial.


```
ABS(x)	returns the absolute value of x
SIGN(x)	returns the sign of input x as -1, 0, or 1 (negative, zero, or positive respectively)
MOD(x,y)	modulo - returns the integer remainder of x divided by y (same as x%y)
FLOOR(x)	returns the largest integer value that is less than or equal to x
CEILING(x) or CEIL(x)	returns the smallest integer value that is greater than or equal to x
POWER(x,y)	returns the value of x raised to the power of y
ROUND(x)	returns the value of x rounded to the nearest whole integer
ROUND(x,d)	returns the value of x rounded to the number of decimal places specified by the value d
SQRT(x)	returns the square-root value of x
```


For example:

```
SELECT round(salary), firstname

FROM employee_info
```

This statement will select the salary rounded to the nearest whole value and the firstname from the employee_info table.



### Joins

Joins can be explained easier by demonstrating what would happen if you worked with one table only, and didn't have the ability to use "joins". This single table database is also sometimes referred to as a "flat table". Let's say you have a one-table database that is used to keep track of all of your customers and what they purchase from your store:



id	first	last	address	city	state	zip	date	item	price
Everytime a new row is inserted into the table, all columns will be be updated, thus resulting in unnecessary "redundant data". For example, every time Wolfgang Schultz purchases something, the following rows will be inserted into the table:

```
id	first	last	address            	city	state	zip	date	item	price
10982	Wolfgang	Schultz	300 N. 1st Ave	Yuma	AZ	85002	032299	snowboard	45.00
10982	Wolfgang	Schultz	300 N. 1st Ave	Yuma	AZ	85002	082899	snow shovel	35.00
10982	Wolfgang	Schultz	300 N. 1st Ave	Yuma	AZ	85002	091199	gloves	15.00
10982	Wolfgang	Schultz	300 N. 1st Ave	Yuma	AZ	85002	100999	lantern	35.00
10982	Wolfgang	Schultz	300 N. 1st Ave	Yuma	AZ	85002	022900	tent	85.00
```

An ideal database would have two tables:

One for keeping track of your customers
And the other to keep track of what they purchase:
"Customer_info" table:

```
customer_number	firstname	lastname	address	city	state	zip
```

"Purchases" table:


```
customer_number	date	item	price
```

Now, whenever a purchase is made from a repeating customer, the 2nd table, "Purchases" only needs to be updated! We've just eliminated useless redundant data, that is, we've just normalized this database!

Notice how each of the tables have a common "cusomer_number" column. This column, which contains the unique customer number will be used to JOIN the two tables. Using the two new tables, let's say you would like to select the customer's name, and items they've purchased. Here is an example of a join statement to accomplish this:

```
SELECT customer_info.firstname, customer_info.lastname, purchases.item

FROM customer_info, purchases

WHERE customer_info.customer_number = purchases.customer_number;
```


This particular "Join" is known as an "Inner Join" or "Equijoin". This is the most common type of "Join" that you will see or use.

Notice that each of the colums are always preceeded with the table name and a period. This isn't always required, however, it IS good practice so that you wont confuse which colums go with what tables. It is required if the name column names are the same between the two tables. I recommend preceeding all of your columns with the table names when using joins.
