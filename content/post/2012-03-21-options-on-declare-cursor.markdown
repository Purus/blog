---
categories:
- Mainframe
- DB2
date: 2012-03-21T06:58:00Z
date_gmt: 2012-03-21 06:58:00 +0530
published: true
status: publish
title: Options on DECLARE CURSOR
---

- Use FOR READ/FETCH ONLY or WITH UR for retrieval only cursors.
- Use OPTIMIZE when you know the accurate number of rows that will be fetched
- Use ORDER BY only when sequence is important
- Use WITH HOLD statement to prevent COMMIT from destroying the cursor position in batch Programs.
- Select only those fields that you truly need
- Use only DCLGEN variables as predicates

While declaring CURSOR in handler we should use OPTIMIZE FOR n ROWS, if we want pass only n rows from DB2 handler back to calling program. In this case DB2 handler only fetches n rows into the intermediate result table. The syntax is

```
DECLARE C1 CURSOR FOR
SELECT * FROM PACS_TRANS_TRACK
OPTIMIZE FOR 5000 ROWS
FOR FETCH ONLY
```

OPTIMIZE FOR tells DB2 to proceed under the assumption that at most a total of integer rows are to be retrieved from the result table. Without this clause, DB2 would assume that all rows of the result table are to be retrieved, and would optimize accordingly. Optimizing for integer rows, if at most this number of rows are fetched, could improve performance.
