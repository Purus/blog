---
categories:
- Mainframe
- File-Aid
date: 2012-01-18T14:37:00Z
date_gmt: 2012-01-18 14:37:00 +0530
published: true
status: publish
title: Easy & Fast Editing of PDS using File-Aid
---

Projects do testing of their code multiple times before they move their code to production. Once the test JCLs are created. From the second run, we need to just change few qualifiers of the DSN and dates in all the JCLs.

The conventional method is enter each member of the JCL PDS and make the changes. If you are sure that you are gonna make common changes in all the members then go ahead and use the below technique.

- Open FILE-AID

- Select *Option 3 UTILITIES*

- Option 6 SEARCH/UPDATE 

- Provide details as present in Below Screen

<a href="http://mainframesf1.files.wordpress.com/2012/01/file-aid11.jpg"><img src="http://mainframesf1.files.wordpress.com/2012/01/file-aid11.jpg"></a>

- If you want to select specific members in PDS, provide “Y” at the option  ”Display member selection list ===>” or else change it to “N”.

<a href="http://mainframesf1.files.wordpress.com/2012/01/file-aid21.jpg"><img src="http://mainframesf1.files.wordpress.com/2012/01/file-aid21.jpg"></a>

- Enter the data that you want to edit (00010101) from after CO and new data to be present (99991231) after EA as shown in the screen. And Press ENTER.

<a href="http://mainframesf1.files.wordpress.com/2012/01/file-aid31.jpg"><img src="http://mainframesf1.files.wordpress.com/2012/01/file-aid31.jpg"></a>

- And then press PF3. The new screen will list out all the changes that will happen if you update.

- Press PF3. In New screen, Provide “Y” at the field “Perform update           ===>” if you would like to perform Update. And press Enter.

<a href="http://mainframesf1.files.wordpress.com/2012/01/file-aid41.jpg"><img src="http://mainframesf1.files.wordpress.com/2012/01/file-aid41.jpg"></a>
