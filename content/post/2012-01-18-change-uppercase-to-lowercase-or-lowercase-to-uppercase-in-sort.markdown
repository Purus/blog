---
categories:
- Mainframe
- DF-Sort
date: 2012-01-18T14:52:00Z
date_gmt: 2012-01-18 14:52:00 +0530
published: true
status: publish
title: Change uppercase to lowercase or lowercase to uppercase in Sort
---

Translation features of INREC, OUTREC and OUTFIL make it easy to change the case of characters in your fields.

The TRAN=LTOU operand can be used to change lowercase EBCDIC letters (a-z) to uppercase EBCDIC letters (A-Z) anywhere in a field.

The TRAN=UTOL operand can be used to change uppercase EBCDIC letters to lowercase EBCDIC letters anywhere in a field.

You could change the case in the entire record as well or part of the record. For example, here's how you could change uppercase to lowercase in the records of an FB data set with an LRECL of 200:

```
OUTREC BUILD=(1,200,TRAN=UTOL)
```

And here's how you could change uppercase to lowercase in the records of a VB data set with any LRECL:

```
OUTREC BUILD=(1,4,5,TRAN=UTOL)
```

Here's how you could change lowercase letters to uppercase letters in a 100-byte character field starting at position 51 in an FB data set with an LRECL of 300:

```
OUTREC BUILD=(1,50,                      1-50: no change 
              51,100,TRAN=LTOU,          51-150: L to U                                    
              151,150)                   151-300: no change
```
