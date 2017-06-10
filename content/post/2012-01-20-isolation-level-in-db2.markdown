---
categories:
- Mainframe
- DB2
date: 2012-01-20T10:40:00Z
date_gmt: 2012-01-20 10:40:00 +0530
published: true
status: publish
title: Isolation level in DB2
---

The list of isoloation leves are listed below.

- SERIALIZABLE(Repeatable read (RR))
- REPEATABLE READ(Read stability (RS))
- READ COMMITTED(Cursor stability (CS)) (default)
- READ UNCOMMITTED(Uncommitted read (UR))

**SERIALIZABLE (DB2 UDB: Repeatable Read)**

Locks the table within a unit of work. An application can retrieve and operate on rows in the table as many times as needed. However, the entire table is locked, not just the rows that are retrieved. Until the unit of work completes, no other application can update, delete, or insert a row that would affect the table.

SERIALIZABLE applications cannot see uncommitted changes made by other applications. Therefore, a SELECT statement issued repeatedly within the unit of work gives the same result each time. Lost updates, access to uncommitted data, and phantom rows are not possible.

**REPEATABLE READ (DB2 UDB: Read Stability)**

Because DB2 Everyplace locks entire tables (not specific rows), REPEATABLE READ behaves exactly like SERIALIZABLE.

**READ COMMITTED (DB2 UDB: Cursor Stability)**

The entire table is locked. Shared locks are released when the associated cursors are closed (isolation levels higher than READ COMMITTED hold shared locks until the end of a transaction). Exclusive locks are held until the end of the transaction.

No other application can perform any DML operation on a table while an open cursor is accessing it. READ COMMITTED applications cannot see uncommitted changes of other applications.

Both non-repeatable reads and phantom reads are possible. READ COMMITTED is the default isolation level, allowing maximum concurrency while seeing only committed rows from other applications.

**READ UNCOMMITTED (DB2 UDB: Uncommitted Read)**

An application can access some uncommitted changes of other transactions: tables and indexes that are being created or dropped by other transactions are not available while the transaction is processing. Any other changes can be read before they are committed or rolled back.

At this level, the application does not lock other applications out of the table it is reading.
