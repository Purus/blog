---
categories:
- Mainframe
- DF Sort
date: 2012-03-21T09:02:00Z
date_gmt: 2012-03-21 09:02:00 +0530
published: true
status: publish
title: Converting a file from VB to FB.
---

DFSORT can be used to do VB to FB conversion, when sorting, copying or  merging. The VTOF or CONVERT and OUTREC operands of OUTFIL can be used  to change variable-length (e.g. VB) input records to fixed-length (e.g.  FB) output records. VTOF or CONVERT indicates that conversion is to be  performed and OUTREC defines the reformatted records. All output data  sets for which VTOF or CONVERT is used must have or will be given  fixed-length record formats.

An example of OUTFIL conversion:

```
//VTOF EXEC PGM=SORT
//SYSPRINT DD SYSOUT=*
//SYSOUT DD SYSOUT=*
//SYSDUMP DD SYSOUT=*
//SORTIN DD DSN=M145.TEMP.SORT.IN,DISP=SHR
//SORTOUT DD DSN=M145.TEMP.SORT.OUT,
             DISP=(NEW,CATLG,DELETE),UNIT=DASD,
             SPACE=(TRK,(500,500),RLSE),
             DCB=(RECFM=FB,LRECL=80)
//SYSIN DD * 
        SORT FIELDS=COPY
        OUTFIL FNAMES=SORTOUT,VTOF,OUTREC=(5,80),VLFILL=C'*'
/*
```

The  above step will copy the records from SORTIN to SORTOUT. If the input  records are shorter than 80 bytes, the output is padded with "*" (Specified by VLFILL).

If VLFILL option is not specified, by default the  records are padded with spaces.

VLFILL=C'x' => pad with the character x.

VLFILL=X'yy' => pad with hexadecimal character X'yy'.
