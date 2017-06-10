---
categories:
- Mainframe
- JCL
date: 2012-01-23T06:12:00Z
date_gmt: 2012-01-23 06:12:00 +0530
published: true
status: publish
title: Run a step only from a set of steps in a job
---

I have a JCL with 20 steps. Due to some reasons I want to execute the step 15 only.

One way to do it is to use RESTART from STEP15, but it will try to execute the subsequent steps too. We have to insert null statement after step15 to prevent the execution of subsequent steps.

But one decent way is there in which we don&rsquo;t need to touch the job steps code, but alter only the Jobcard.

And that is....

In the JOBCARD, code COND parameter. Then, when the Job is executed , only the Step mentioned in the RESTART parameter will get executed.

```
RESTART=STEP15,COND=(0,LE)
```
