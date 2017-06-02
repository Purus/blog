---
categories:
- JCL
- Mainframe
date: 2013-08-02T09:00:00Z
date_gmt: 2013-08-02 03:30:00 +0530
published: true
status: publish
tags:
- jcl
- mainframe
- steps
title: Overriding Concatenated Datasets in JCL
url: /2013/08/02/overriding-concatenated-datasets-in-jcl/
---

Lets assume that you have a PROC with the following step which has 5 concatenated steps.

{{< highlight jcl >}}
//STEP010 EXEC PGM=PROGRAM1  
//INPUTF      DD DSN=INPUT.FILE1,DISP=SHR  
//            DD DSN=INPUT.FILE2,DISP=SHR  
//            DD DSN=INPUT.FILE3,DISP=SHR  
//            DD DSN=INPUT.FILE4,DISP=SHR  
//            DD DSN=INPUT.FILE5,DISP=SHR
{{< / highlight >}}

In the JCL which calls the above mentioned PROC, you want to override only one of the 5 concatenated files from PROC. For example, you want to override the 3rd concatenated file with another file called INPUT.NEWFILE in the JCL.

This can be accomplished by using the below code in your JCL where you want to override the file.

{{< highlight jcl >}}
//STEP010.INPUTF   DD  
//                 DD  
//                 DD DSN=INPUT.NEWFILE,DISP=SHR  
//                 DD  
//                 DD
{{< / highlight >}}

Please not that you can not use DUMMY statement, as the usage of DUMMY signifies END OF FILE statement and will ignore the next coming files.
