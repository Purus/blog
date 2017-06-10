---
categories:
- Mainframe
- ISPF
date: 2012-01-19T20:07:00Z
date_gmt: 2012-01-19 20:07:00 +0530
published: true
status: publish
title: Repeating the ISPF command without typing again
---

Any command entered in the ISPF COMMAND LINE disappears after the successful execution of its intended function. If you want to repeat the same command , you got to re-type it or use some PF key to retrieve the last command entered.<br>

But here is a cool method the make the command entered not to disappear and stay on the screen.

Precede commands with "&".

**For Example:**

>&C  '110-PARA'  '220-PARA'

After the execution of the command, the below command stays on the screen.

This way you can entering the same command or modifying the command a little and using it multiple times.
