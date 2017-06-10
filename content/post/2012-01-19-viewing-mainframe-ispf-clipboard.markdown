---
categories:
- Mainframe
- ISPF
date: 2012-01-19T20:57:00Z
date_gmt: 2012-01-19 20:57:00 +0530
published: true
status: publish
title: Viewing Mainframe ISPF Clipboard
---

When I issue CUT , I know that the CUT content are placed in a clipboard. And when I issue PASTE, the clipboard content are pasted.<br>

But is it possible for me to view and edit the clipboard?<br>

One can view the clipboard after any valid CUT command was issued.<br>

To view the clipboard, issue : 

```
CUT DISPLAY
```

<br>Clipboard manager will pop up and gives us options to edit or browse the content.
