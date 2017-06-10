---
categories:
- Mainframe
- ISPF
date: 2012-01-23T06:30:00Z
date_gmt: 2012-01-23 06:30:00 +0530
published: true
status: publish
title: ISPF Special Searching
---

A picture string in a FIND, CHANGE, or EXCLUDE command allows you to search for a particular kind of character without regard for the specific character involved.

You can use special characters within the picture string to represent the kind of character to be found, as follows:

They can be used in REXX ISREDIT macros too. 

|String | Meaning |
|-------|---------|
|P'='  | Any character|
|P'&not;' |  Any character that is not a blank||
|P'.' | Any character that cannot be displayed|
|P'#' | Any numeric character, 0-9|
|P'-' | Any non-numeric character|
|P'@' | Any alphabetic character, uppercase or lowercase|
|P'c' | Any lowercase alphabetic character|
|P'>' | Any uppercase alphabetic character|
|P'$' | Any special character, neither alphabetic nor numeric|
