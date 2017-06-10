---
categories:
- Mainframe
- DF Sort
date: 2012-01-18T12:50:00Z
date_gmt: 2012-01-18 12:50:00 +0530
published: true
status: publish
title: Add leading and trailing Characters in Sort
---

Lets assume that we have a sequential dataset with records as below:

```
ONE
TWO
THREE
FOUR
FIVE
```

I want to reformat the records for output as follows:

```
NUMBER 'ONE'
NUMBER 'TWO'
NUMBER 'THREE'
NUMBER 'FOUR'
NUMBER 'FIVE'
```

You can do this quite easily with DFSORT's JFY function as follows:

> OPTION COPY
>
> INREC BUILD=(1,13,JFY=(SHIFT=LEFT,LEAD=C'NUMBER ''', TRAIL=C'''')

SHIFT=LEFT left-justifies the data. LEAD inserts the hard coded text NUMBER ' before the value with no intervening blanks.
 
TRAIL inserts ' after the value with no intervening blanks.
