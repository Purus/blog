---
categories:
- Mainframe
- File-Aid
date: 2012-01-20T10:14:00Z
date_gmt: 2012-01-20 10:14:00 +0530
published: true
status: publish
title: Find bad data using File-Aid
---

The Easiest and Coolest way to locate bad data is thru File-Aid's FIND command.

- OPEN the file in FILE-AID (in either browse or edit mode).
- XREF with COPYBOOK. 
- Use FMT mode. 
- Then issue the below command.

>F /field-name INVALID 

or

> F /field-number INVALID

The control will take you to the first invalid data record for the given field.

Example: The FILE has 3 fields namely NAME,AGE,COUNTRY. If you want to find the invalid data in the age field, then issue F /2 INVALID.
