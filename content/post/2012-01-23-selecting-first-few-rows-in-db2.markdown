---
categories:
- Mainframe
- DB2
date: 2012-01-23T11:58:00Z
date_gmt: 2012-01-23 11:58:00 +0530
published: true
status: publish
title: Selecting first few rows in DB2
---

DB2's method of performing a Top-N query is the FETCH FIRST clause. You can append these variations to a regular SELECT query:

- FETCH FIRST ROW ONLY  
- FETCH FIRST 1 ROW ONLY
- FETCH FIRST integer ROWS ONLY 

Interestingly, you can also use:

- FETCH FIRST 1 ROWS ONLY
- FETCH FIRST 5 ROW ONLY 

They aren't as nice  grammatically, but they make it easier to generate queries automatically - you don't have to worry about whether to say ROW or ROWS.

Now, we can ask for a single record as follows:

**Listing 1** - Return a Single Row

```
SELECT * FROM MYSALES 
FETCH FIRST ROW ONLY
```

|CLIENT  |   MONTHEND     |SALEVOL | 
|--------|----------------|--------|
|DEVX    |   03/31/1998   |  100   |

We have retrieved one row, but there's no way to know ahead  of time which row it will be.

> This does give us a handy way to  remind ourselves what fields are in a table, with a row of sample data  as a bonus!

**Listing 2** - Show Top Two Clients 

```
SELECT CLIENT, SUM(SALEVOL) AS TOTALVOL
FROM MYSALES 
GROUP BY CLIENT 
ORDER BY SUM(SALEVOL) DESC
FETCH FIRST 2 ROWS ONLY
```

|CLIENT   |  TOTALVOL |  
|---------|-----------|
|DEVX     |      5785 |  
|EGGHEAD  |      5341 |

