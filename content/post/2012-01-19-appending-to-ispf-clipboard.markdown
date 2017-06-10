---
categories:
- Mainframe
- ISPF
date: 2012-01-19T21:02:00Z
date_gmt: 2012-01-19 21:02:00 +0530
published: true
status: publish
title: Appending to ISPF Clipboard
---

Scenario:
---------

I have a dataset with 10,000 lines. I want to cut the first 10 lines and last 10 lines and paste into another dataset. When I cut the first 10 lines and then again the last 10 lines, only the last 10 lines are pasted into the new dataset.

<br>Is there anyway out (other than doing a 2 cut & paste)?

<br>Yes, here it is.<br>

<ol>
<li>First cut 10 lines, then issue CUT APPEND.</li>
<li>Cut last 10 lines, then issue CUT APPEND.</li>
<li>When you PASTE it, you got both.</li>
</ol>

