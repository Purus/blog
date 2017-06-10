---
categories:
- Mainframe
- ISPF
date: 2012-03-21T08:59:00Z
date_gmt: 2012-03-21 08:59:00 +0530
published: true
status: publish
title: Recovering Deleted Flat Files in Mainframe
---

Flat files can be recovered by following the below mentioned steps.

- Start 6
- HLIST BCDS DSN('filename')
- Wait for the system notification
- Type the command **HRECOVER 'filename'** and wait for system notification

Different variations of HRECOVER are given below.

- HRECOVER 'filename' : recovers with same name.
- HRECOVER 'old filename' NEW ('new filename') : recovers and assigns new name.
- HRECOVER 'file name' REPLACE : recovers replacing a file with same name.

The recovery might take some time. You should have HSM volume dump(s) of the volume(s) where the dataset resided for HRECOVER to work successfully. Else you will recive a message "BACKUP DUMP COPY DOES NOT EXIST".
