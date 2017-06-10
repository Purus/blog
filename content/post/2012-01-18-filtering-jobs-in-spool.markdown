---
categories:
- Mainframe
- SDSF
date: 2012-01-18T15:25:00Z
date_gmt: 2012-01-18 15:25:00 +0530
published: true
status: publish
title: Filtering Jobs in Spool
---

There is a possibility to list only the jobs which has ABENDED, leaving out all other jobs in the spool.

For such a kind of listing, use the primary command FILTER on the command line as given in the examples below.

```
FIL MAX AB* - shows jobs that has ABENDS
```

*Other Examples are:*

Shows jobs that has JCL errors:
```
FIL MAX ‘JCL ERROR’
```

Shows jobs with “exceptional conditions”:
```
FIL MAX NE ‘RC 0000’
```

Shows successfully completed jobs:
```
FIL MAX EQ ‘RC 0000’
```

If you want to switch off the filter, then issue FIL OFF.
