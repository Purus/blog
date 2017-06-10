---
categories:
- Mainframe
- DB2
date: 2012-01-20T10:46:00Z
date_gmt: 2012-01-20 10:46:00 +0530
published: true
status: publish
title: Like the DB2 LIKE
---

The LIKE phrase defines a mask for comparing characters:

```
WHERE COL_VAL [NOT] LIKE mask
```

A mask may be a host variable or a literal enclosed in quotes and may contain any number of:

| Mask | What to Find? |
| ------------- | ------------- |
| character literal | for an exact match  |
| underscore character | for any single character  |
|percent   sign character|for   any sequence of characters of length 0 or more|

For example:

|Mask | Example Outout|
| ------------- | ------------- |
|'NEW %'| NEW YORK’ but not ‘NEWARK’|
|'T_N' | 'TAN', 'TIN', or 'TON', but not 'TUNE'|
|'T_N%'|'TUNE'|
|'%CA%'|'CAT', 'GO CART', 'MOCA', etc.|
|'%CA% '|'CAT ' but not 'CAT'|



To use a host variable for a mask to produce the same effect as the literal mask in the second-to-last example, code it right-padded with “%” characters to avoid the effect of the last example.

```
05  WS-MASK           PIC  X(6)  VALUE ‘%CA%%%’.
```

The IN phrase chooses from a given set:

```
WHERE COL_VAL [NOT] IN (:HOST-VAR, ‘LITERAL’, COL1 + COL2, …)
```

Multiple list items that contain the same value are considered as a single item. The BETWEEN phrase chooses from a range of inclusive limits:

```
WHERE COL_VAL [NOT] BETWEEN [:HOST-VAR1, ‘LIT1’]
                           AND [:HOST-VAR2, ‘LIT2’]
```                           
