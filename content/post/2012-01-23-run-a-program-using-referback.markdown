---
categories:
- Mainframe
- JCL
comments: []
date: 2012-01-23T06:02:00Z
date_gmt: 2012-01-23 06:02:00 +0530
published: true
status: publish
title: Run a Program using Referback
---

It is possible to execute a program from any library using the referback feature.

```
STEP1 EXEC PGM=IEFBR14
//PROGRAM DD DSN=SYSTEM.PGM.LOADLIB(COBOLPGM),DISP=SHR
.
.
.
.
.
//STEP2 EXEC PGM=*.STEP1.PROGRAM
```
