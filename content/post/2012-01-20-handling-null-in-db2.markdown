---
categories:
- Mainframe
- DB2
date: 2012-01-20T10:43:00Z
date_gmt: 2012-01-20 10:43:00 +0530
published: true
status: publish
title: Handling NULL in DB2
---

The value of an indicator variable tells the status of a row after a query.

*Host Variable*:

```
01 FILLER.
   05 WS-AMOUNT  PIC S9(5)V9(2) COMP-3.
   05 WS-CUSTNUM PIC X(5). 
```

*Indicator variable*:

```
01 FILLER. 
   05 AMT-IND PIC S9(4) COMP. 
```

Consider the below SQL.

```
EXEC SQL
   SELECT CUST_AMOUNT 
   INTO :WS-AMOUNT:AMT-IND
   FROM T100.CUST 
   WHERE CUST_ID = :WS-CUSTNUM 
 END-EXEC. 
```

After a query, the indicator variable contains the following:

- 0 -  Column is not null
- -1 -  Column is null
- -2 -  Column is null as result of conversion error 
- +length - Full length of column that was truncated to fit a short host variable 

**Some points to ponder**:

- Load -1 to the indicator variable to set a column to a null value, during UPDATE or INSERT of a row. 
- If a column is always to be set to a null value, code the NULL keyword for the column in the UPDATE statement's SET clause or in the INSERT statement's VALUES clause. 
- A column omitted from the row list of an INSERT statement will always be set to a null value, if the column was defined as NOT NULL; otherwise, an error will occur. 
- Code a predicate to test for null with the following syntax:

> WHERE column name IS [NOT] NULL

The scalar functions, VALUE and COALESCE, are equivalent, and they can be used only in outer joins; each takes a list of multiple parameters and returns the first parameter that is not null.  

The following will return either a non-null column value or a literal:

```
EXEC SQL
 SELECT ACCT_REG,VALUE(ACCT_A1, ACCT_A2, ‘NO ACCT’) 
 INTO :WS-REGION
     ,:WS-ACCOUNT
 FROM REGS.TABLE_EMP
 WHERE ACCT_REG <> ’65’
END-EXEC.
```
