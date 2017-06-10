---
categories:
- Mainframe
- DB2
date: 2012-01-18T18:10:00Z
date_gmt: 2012-01-18 18:10:00 +0530
published: true
status: publish
title: Verification of DB2 Consistency token
---

When a Job abends at a program due to bind error with SQL code of -805 or -818 then generally there is issue with consistency token (often referred as CONTOKEN). These kind of abends can be easily fixed if we can find where the CONTOKEN mismatch occurs.

**STEP1**:- CONTOKEN in Package

RUN the following query:

>SELECT NAME, CONTOKEN, COLLID, PDSNAME FROM SYSIBM.SYSPACKAGE
>WHERE NAME='MODULE'
>AND COLLID='COLLID'

Provide the name of the module in "*NAME*" and Collection name in "*COLLID*".

In the Query output dataset locate the CONTOKEN value and view it in HEX mode (by issuing HEX ON command)

Lets assume the HEX contoken in the above example to be as:

>1DE6102A
>8A19F405

which is to be read as:
> 18DAE1691F0420A5

**STEP2**:- CONTOKEN in DBRMLIB

The "PDSNAME" field above will indicate the DBRMLIB used for binding the module.

- Goto the DBRMLIB
- Open the DBRM for the above module, it will have the same name as the module name.
- Search for the contoken in hex mode by entering the following command

> F X'18DAE1691F0420A5'

<img alt="CONTOKEN IN DBRM IN DBRMLIB" src="/uploads/contoken2.JPG">

(The CONTOKEN in the DBRM is generally at the 25th position as shown in the figure above)

>**Note:-**
>     If the CONTOKEN in Step1 and Step2 does not match then Run the Bind job to fix the inconsistency. Bind Job is going  to update the CONTOKEN in the SYSIBM.SYSPACKAGE Table.

**STEP3**:- CONTOKEN in loadlib

Since the date and time part of the CONTOKEN are swapped in loadlib, you will have to split the CONTOKEN found in SYSPACKAGE table in two halves of 8 chars each and then swap their positions.

First Half
>18DAE169

Second Half
>1F0420A5

Swapping positions and joining them back will result in the CONTOKEN

>1F0420A518DAE169

- Go to the load library where the load to be checked is present. CONTOKEN in Composite load of the link.

- Open the load object for the program, it generally has the same name as the module name.

- Now search for the reversed CONTOKEN in hex mode in the load of the program using command.

>F X'1F0420A518DAE169'

<img alt="CONTOKEN in load object in LOADLIB" src="/uploads/contoken3.jpg"

Note:- If the CONTOKEN is found then its fine and if not then you will need to recompile and also relink(if composite load also doesnt has this) to fix the issue.

**Source**: Mainframe Wizard
