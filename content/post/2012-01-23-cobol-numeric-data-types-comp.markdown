---
categories:
- COBOL
comments: []
date: 2012-01-23T10:38:00Z
date_gmt: 2012-01-23 10:38:00 +0530
published: true
status: publish
title: COBOL Numeric Data Types-COMP
---

The following common COBOL data types are discussed below:

- Binary
- Computational (comp)
- Comp-1
- Comp-2
- Comp-3
- Packed Decimal

**BINARY **

Specified for binary data items. Such items have a decimal equivalent consisting of the decimal digits 0 through 9, plus a sign. Negative numbers are represented as the two’s complement of the positive number with the same absolute value.  The amount of storage occupied by a binary item depends on the number  of decimal digits defined in its PICTURE clause:

Digits in PICTURE Clause Storage Occupied 
1 through 4 2 bytes (halfword) 
5 through 9 4 bytes (fullword) 
10 through 18 8 bytes (doubleword) │ 
The leftmost bit of the storage area is the operational sign.

**PACKED-DECIMAL** 
Specified for internal decimal items. Such an item appears in storage  in packed decimal format. There are 2 digits for each character  position, except for the trailing character position, which is  occupied by the low-order digit and the sign. Such an item can  contain any of the digits 0 through 9, plus a sign, representing a  value not exceeding 18 decimal digits.

The sign representation uses the same bit configuration as the 4-bit  sign representation in zoned decimal fields.

**COMPUTATIONAL or COMP** 
Representation of the COMPUTATIONAL phrase is system-dependent and is  normally assigned to representations that yield the greatest  efficiency when arithmetic operations are performed on that system.

**COMPUTATIONAL-1 or COMP-1**
Specified for internal floating-point items (single precision).  COMP-1 items are 4 bytes long. The sign is contained in the first bit  of the leftmost byte and the exponent is contained in the remaining 7  bits. The last 3 bytes contain the mantissa.

**COMPUTATIONAL-2 or COMP-2** 
Specified for internal floating-point items (double precision). COMP-2 items are 8 bytes long. The sign is contained in the first bit  of the leftmost byte and the remaining 7 bits contain the exponent.  The remaining 7 bytes contain the mantissa.

**COMPUTATIONAL-3 or COMP-3** (internal decimal) 
For VS COBOL II, this is the equivalent of PACKED-DECIMAL.

**COMPUTATIONAL-4 or COMP-4 (binary) **
For VS COBOL II this is the equivalent of BINARY.
