---
categories:
- Mainframe
- VSAM
date: 2012-01-20T10:32:00Z
date_gmt: 2012-01-20 10:32:00 +0530
published: true
status: publish
title: Read Only VSM Files
---

By using INHIBIT along with ALTER command, we can have a read-only VSAM dataset.

Example:

```
//STEP1 EXEC PGM=IDCAMS
//SYSPRINT DD SYSOUT=*
//SYSIN DD *
ALTER –
SECRET.KSDS.DATA –
INHIBIT
ALTER –
SECRET.KSDS.INDEX –
INHIBIT
/*
```

Notice that the ALTER command is used with DATA and INDEX and not with the cluster.
