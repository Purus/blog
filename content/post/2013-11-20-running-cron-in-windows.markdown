---
categories:
- Computers
date: 2013-11-20T23:57:16Z
date_gmt: 2013-11-20 18:27:16 +0530
published: true
status: publish
title: 'Running Cron in Windows '
---

We all would have heard of Cron jobs, if you are involved in website management, development or working on Linux/Unix machines.

**What's a cron?**

> Cron is nothing but an demon job running in the background without any user intervention. It gets executed automatically based on the predefined time interval.

Generally cron jobs are used to perform some maintenance activities in the server. For example, if you run a very popular blog, you can use the cron job to send out a weekly mail to all the users about the new blog posts. Or even removing any unwanted file uploads once a month. It's not very unusual to link cron to *nix machines.

But coming to the reality, not all web developers(like me) work on *nix machines. I use WAMP stack for development and testing of my PHP projects. I often need to setup a cron for some important activities related to my applications. There is no direct way of setting up cron in your XAMP or XAMPP installation in Microsoft Windows.

Microsoft has included a tiny command line utility called "Task Scheduler" in its Windows Operating Systems. We invoke that utility by running schtasks.exe command.

**Listing all current scheduled tasks** 

> In your Windows command prompt, type "schtasks" (without quotes) and press the Enter key. You can see the list of scheduled tasks in your machine.  

<a href="/uploads/schtasks-status.png"><img src="/uploads/schtasks-status.png"></a>

**Adding a new scheduled task**

To add a new task, you can use "schtasks /create" command. For example the below command, makes the scheduler to run the php file "run.php" every 1 minute. 

> schtasks /create /sc minute /mo 1 /tn "My Cron" /tr "php -f C:\wamp\www\oxwall\ow_cron\run.php"

<a href="/uploads/schtasks-add.png"><img src="/uploads/schtasks-add.png"></a>

> It might ask for your windows password if necessary.

The breakup of the above command are provided below.

 -  /sc - defines the schedule type. Possible values are MINUTE, HOURLY, DAILY, WEEKLY, MONTHLY, ONCE, ONSTART, ONLOGON, ONIDLE
 -  /mo - defines how often the task runs within its schedule type (Example : every minute, every day, or weekly once).
 -  /tn - gives your task a name to easily identify
 -  /tr - command or utility to be ran

Once you are done, you could see the command prompt opening and closing for every minute as I set my cron for 1 minute. If you list down the tasks, you could see the new task added to the list.
  
**Deleting an existing task**
To delete the task you can follow the below example.

> schtasks /delete /TN "My Cron"

I have tested in my Windows machine and this should work for all other advanced versions too. For advanced options on modifiers please refer to [Microsoft Windows Product Documentation](http://www.microsoft.com/resources/documentation/windows/xp/all/proddocs/en-us/schtasks.mspx?mfr=true)

***
