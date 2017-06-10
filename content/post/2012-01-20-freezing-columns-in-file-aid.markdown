---
categories:
- Mainframe
- File-Aid
date: 2012-01-20T10:38:00Z
date_gmt: 2012-01-20 10:38:00 +0530
published: true
status: publish
title: Freezing columns in File-Aid
---

While working in MS Excel we have the option of "Freeze Panes". By this options we can freeze some columns and have other columns scrolling. This feature is helpful in analysis when there are lots of columns(fields) in a file.

In mainframe too, we have similar such facility thru File-Aid.

- Open the file in File-Aid
- Use VFMT format
- If you want to freeze columns(fields) 1,2,3, and 6 and have the rest as scrollable issue the below command.

> HOLD 1-3,6 
