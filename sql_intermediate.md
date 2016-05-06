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
