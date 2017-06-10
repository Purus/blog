---
categories:
- File-Aid
comments: []
date: 2012-01-18T18:30:00Z
date_gmt: 2012-01-18 18:30:00 +0530
published: true
status: publish
tags: []
title: Copy a Dataset using File-Aid
---

<p>The steps to copy a file using File-Aid are :<br>
<ol><br>
<li>Go to TSO&#47;ISPF<&#47;li><br>
<li>Open fileaid giving command as per your shop&rsquo;s configuration<&#47;li><br>
<li>Once FileAid&rsquo;s Primary Option Menu is opened<&#47;li><br>
<li>Choose Utilities<&#47;li><br>
<li>Choose Copy<&#47;li><br>
<li>Give source PDS&#47;dataset name (in FROM ) you might need to provide volume serial number if it is not cataloged.<&#47;li><br>
<li>Give destination PDS&#47;dataset name (in TO) you might need to provide volume serial number if it is not cataloged.<&#47;li><br>
<li>Choose the Disposition New if your <strong>TO<&#47;strong> is new dataset <strong>OLD <&#47;strong>for existing dataset<&#47;li><br>
<li>Specify the properties of new dataset in &ldquo;<strong>Allocate New SMS Dataset<&#47;strong>&rdquo; It has to be similar to soure (record length&#47;size&#47;etc<&#47;li><br>
<li>If you are copying form a PDS then it will ask which all members you want to copy to destination.<&#47;li><br>
<li>Select members you want to copy and then hit return to confirm the members you have selected.<&#47;li><br>
<li>PF3 out and see the message top right corner for the status of your operation.<&#47;li><br><&#47;ol></p>
