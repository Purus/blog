---
categories:
- Mainframe
- DB2
date: 2012-01-23T06:09:00Z
date_gmt: 2012-01-23 06:09:00 +0530
published: true
status: publish
title: DB2 Index with Expressions
---

Prior to DB2 9, the create index statement only allowed you to use the column name from the table the index is being built on. The same value for each column stored on the table was copied into the index and used to quickly identify the row when searching by that column name. Now with DB2 9, the create index statement supports a feature known as key expressions. Here’s why key expressions should interest you.

Many times when you’re writing complex queries, you’d like to the optimizer to use an index, but instead it performs a table space scan. These situations usually occur when you’re using scalar functions or arithmetic calculations. Let’s consider a couple of examples:
Say you have a column on the table called lastname and the data in this column is stored in lowercase. But because end users can enter last names in upper and lower case, you must convert everything to upper case to perform the search. The following sample contains DDL to create an index on the table EMPL and then SQL to search for employees with a last name of ‘COLEMAN’.

```
CREATE INDEX EMPL_X1 ON EMPL
  (lastname);
  
SELECT EMPNO, FIRSTNME, LASTNAME, SALARY, BONUS, COMM
FROM EMPL
WHERE UPPER(lastname) = ‘COLEMAN’
```

No match: In this sample, DB2 cannot use index EMPL_X1 because of the scalar function UPPER. To resolve this in DB2 9, you can use an expression to store the data in the index as upper case.

```
CREATE INDEX EMPL_X2 ON EMPL
  UPPER(lastname);
```

Now DB2 can use index EMPL_X2 and match on the data.

Next is is an example of the types of queries you’d see in a data decision support or data warehousing application. Say you need to present a list of employees that have a total compensation package greater than $12,000 a month. The compensation package is made up of salary, bonus and commission. In DB2 8 your index on the columns may be defined this way:

```
CREATE INDEX EMPL_X3 ON EMPL
  (salary, bonus, comm);
  
SELECT EMPNO, FIRSTNME, LASTNAME, SALARY, BONUS, COMM
FROM EMPL
WHERE salary + bonus + comm. > 12000.00
```

However, due to the arithmetic calculations in the where clause, the optimizer cannot use the EMPL_X3 index to retrieve all employees making more than $12,000. With DB2 9 though you can create an index with the expression to calculate the total and store this in the index. The optimizer can now match on the column because the data was precalculated and stored in the index. Index EMPL_X4 shows how you’d use a key expression to calculate and store the results in an index.

```
CREATE INDEX EMPL_X4 ON EMPL
  (salary + bonus + comm);
```

If you’re going to use expressions, consult the DB2 9 SQL Reference guide. A list of rules and restrictions can be found under the CREATE INDEX statement.

The basic rule is that you must reference at least one column from the table. The column named must not be of type LOB, XML or DECFLOAT. The referenced columns cannot include any FIELDPROCs or a SECURITY LABEL.

Also, key expressions must not include:

- A subquery — an aggregate function
- A not deterministic function
- A function that has an external action
- A user-defined function
- A sequence reference
- A host variable
- A parameter marker
- A special register
- A CASE expression
- An OLAP specification
