---
categories:
- Mainframe
- DB2
date: 2012-01-23T12:01:00Z
date_gmt: 2012-01-23 12:01:00 +0530
published: true
status: publish
title: Ranking and Numbering for Records in DB2
---

DB2 supports ranking and numbering in much the same way that Oracle does.

The available functions are:

- ROW_NUMBER(), which simply numbers the returned rows sequentially  <&#47;li>
- RANK(), which ranks the results, but, in the case of a tie, gives the same number to each and leaves a gap to compensate  <&#47;li>
- DENSE_RANK() operates the same as RANK() but doesn't leave any gaps. 

**Listing 1** - Ranking and Numbering Results

```
select 
client, MONTHEND, SALEVOL, 
ROW_NUMBER() over (order by SALEVOL desc) AS RN, 
RANK() over (order by SALEVOL desc) AS RANK, 
DENSE_RANK() over (order by SALEVOL desc) AS DENSE
from mysales
where MONTHEND=DATE('1997-11-30')
order by RN
```

|CLIENT   | MONTHEND   | SALEVOL | RN | RANK |DENSE|
|---------|------------|---------|----|------|-----|
|CYRIX    | 11/30/1997 | 120     | 1 |  1  |  1|  
|BIG BLUE | 11/30/1997 | 106     | 2 |  2  |  2|  
|EGGHEAD  | 11/30/1997 | 106     | 3 |  2  |  2| 
|DEVX     | 11/30/1997 | 80      | 4 |  4  |  3| 
|FIGTREE  | 11/30/1997 | 62      | 5 |  5  |  4|
|ACME     | 11/30/1997 | 20      | 6 |  6  |  5|


The results need not be returned in rank order. We may wish to show each client's rank while listing them alphabetically.

**Listing 2** -  Return Ranks in Any Order

```
select
CLIENT, SALEVOL,
RANK() over (order by SALEVOL desc) AS RANK
from mysales
where MONTHEND=DATE('1997-11-30')
order by CLIENT
```

|CLIENT   |  SALEVOL |RANK|   
|---------|----------|----|
|ACME     |       20 |   6|  
|BIG BLUE |      106 |   2|
|CYRIX    |      120 |   1|  
|DEVX     |       80 |   4|
|EGGHEAD  |      106 |   2|   
|FIGTREE  |       62 |   5|


One application of ROW_NUMBER is to select a numbered range  of rows from the middle of your results. For example, you could  retrieve the next three clients following the top two.

**Listing 3** - Selecting Rows by Number 

```
WITH ALLSALES AS 
(SELECT CLIENT, SUM(SALEVOL) AS TOTALVOL,
ROW_NUMBER() OVER
(ORDER BY SUM(SALEVOL) DESC, CLIENT)
AS RN
FROM MYSALES 
GROUP BY CLIENT)

SELECT
CLIENT, TOTALVOL, RN
FROM ALLSALES
WHERE RN BETWEEN 3 AND 5
ORDER BY RN
```

|CLIENT   |  TOTALVOL  |RN|
|---------|------------|--|
|BIG BLUE |      4781  | 3|
|FIGTREE  |      3986  | 4|
|ACME     |      3044  | 5|

