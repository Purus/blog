---
categories:
- Mainframe
- JCL
date: 2012-01-23T06:16:00Z
date_gmt: 2012-01-23 06:16:00 +0530
published: true
status: publish
title: TIME=NOLIMIT and TIME=MAXIMUM
---

We can specify the max limit of TIME parameter as

TIME=NOLIMIT 

TIME=MAXIMUM

Now which specification gives maximum time for a JOB?

TIME=MAXIMUM will allow the job to run for 357912 minutes (248.55 days)

TIME=NOLIMIT will allow the job for unlimited amount of time

Another advantage of NOLIMIT option is that it can remain in wait status for more than the installation time limit.
