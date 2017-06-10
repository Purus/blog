---
categories:
- Mainframe
- Sort
date: 2013-06-26T15:30:00Z
date_gmt: 2013-06-26 10:00:00 +0530
published: true
status: publish
title: Replacing low values to spaces in Mainframe Sort
---

In Mainframe, using Sort, how can I replace all the low-values in a file to spaces?

We can use ALTSEQ CODE to change the low-values or high-values to spaces in a file using Sort.
Here's an example of how you could change all low values (X'00') to spaces (X'40'), in an FB data set with an LRECL of 80:

{{< highlight jcl >}}
ALTSEQ CODE=(0040)
OUTREC FIELDS=(1,80,TRAN=ALTSEQ)
{{< / highlight >}}
