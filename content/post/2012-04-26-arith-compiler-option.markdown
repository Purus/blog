---
categories:
- Mainframe
- COBOL
date: 2012-04-26T09:08:00Z
date_gmt: 2012-04-26 03:38:00 +0530
published: true
status: publish
title: ARITH Compiler Option in COBOL
---

ARITH affects the maximum number of digits that you can code for integers, and the number of digits used in fixed-point intermediate results. By specifying ARITH complier option we can control the maximum number of digits allowed for decimal numbers (packed decimal, zoned decimal and numeric-edited data items and numeric literals).

- ARITH(EXTEND)  :  Max. Number of digits 31.

- ARITH(COMPAT) : Max. Number of digits 18.

Default is: ARITH(COMPAT)

Abbreviations are: AR(C|E)

Arith-extend is performance hampering because of larger intermediate results.

When you specify ARITH(EXTEND):

- The maximum number of digit positions that you can specify in the PICTURE clause for packed-decimal, external-decimal, and numeric-edited data items is raised from 18 to 31.
- The maximum number of digits that you can specify in a fixed-point numeric literal is raised from 18 to 31. You can use numeric literals with large precision anywhere that numeric literals are currently allowed, including:
   - Operands of PROCEDURE DIVISION statements
   - VALUE clauses (for numeric data items with large precision PICTURE)
   - Condition-name values (on numeric data items with large-precision PICTURE)
- The maximum number of digits that you can specify in the arguments to NUMVAL and NUMVAL-C is raised from 18 to 31.
- The maximum value of the integer argument to the FACTORIAL function is 29.
- Intermediate results in arithmetic statements use extended mode.

When you specify ARITH(COMPAT):

- The maximum number of digit positions in the PICTURE clause for packed-decimal, external-decimal, and numeric-edited data items is 18.
- The maximum number of digits in a fixed-point numeric literal is 18.
- The maximum number of digits in the arguments to NUMVAL and NUMVAL-C is 18.
- The maximum value of the integer argument to the FACTORIAL function is 28.
- Intermediate results in arithmetic statements use compatibility mode.
