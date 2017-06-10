---
categories:
- JCL
- VSAM
date: 2012-01-20T10:28:00Z
date_gmt: 2012-01-20 10:28:00 +0530
published: true
status: publish
title: Dummy VSM Dataset in JCL
---

In general we use DUMMY datasets in JCL instead of a actual file for some requirements.

But how can we specify dummy VSAM dataset in a JCL?

The parameter AMP='AMORG' tells the OS to treat the file as VSAM file. 

>//NOVSAMIO DD DUMMY,AMP='AMORG'
