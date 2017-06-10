---
categories:
- Computers
date: 2013-10-25T22:42:36Z
date_gmt: 2013-10-25 17:12:36 +0530
published: true
status: publish
title: Solution for Disk Drive Full error with USB Pen Drives
---

When you copy large files (greater than 3 GB) to your USB pen drive, it's almost sure that you will get an error alerting that "Disk drive is full". I am sure you will be surprised on seeing this error as your USB pen drive will have more than 10 GB available. I swear, I did got surprised. I confirmed that my USB drive has enough space.

I spend some time on finding out why this happens. And yet again it's one of the mysteries of Windows OS. The reason behind this is that the USB device is in FAT32 file system and has some limitations. NTFS file system is not enabled on the devices to support high performance. The default option is to support quick removal of device.

> I am using Windows XP and I assume this solution should work for any other Windows Operation Systems. Please correct me if my assumption is wrong.

Ok.. here is the solution.

1.  Right click on the USB drive having this problem in the Windows Explorer.
2.  Select "Properties".
3.  Click the "Hardware" tab in the property dialog box.
4.  Find the USB drive disk in the list and double click it.
5.  Click the "Policies" tab.
6.  Select "Optimize for performance" and click "OK" button to close the dialog.

>  As you have now enabled "Optimize for performance", you have disabled "Option for quick removeal" feature. So you should always remove your USB device by selecting "Safely Remove" option. 

After these step, you can format your USB drive to NTFS file system. All the above steps are shown with actual images.

<a href="/uploads/1.png"><img src="/uploads/1.png"></a>

<a href="/uploads/2.png"><img src="/uploads/2.png"></a>

<a href="/uploads/3.png"><img src="/uploads/3.png"></a>

<a href="/uploads/4.png"><img src="/uploads/4.png"></a>

