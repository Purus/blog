---
categories:
- Mainframe
- JCL
date: 2012-02-09T07:32:00Z
date_gmt: 2012-02-09 07:32:00 +0530
published: true
status: publish
title: GDG - A Basic Introduction
---

**Introduction**

GDG stands for Generation Data Group. Here a group of files are related functionally or chronologically and can be accessed individually or as a group. These files share a unique name.

- Every dataset in a GDG has a Generation number and version number. Eg.TESTGDG.DATA.G0001.V00
- Subsequent files are named by incrementing the Generation number(G0001-G9999).
- The current generation is referred a 0. The next generation as +1 an previous generation as -1
- Every time a new gen is created, it becomes the current gen and the current gen becomes the previous generation.
- All generations must be cataloged to keep track of the relative generation  numbers
- Maximum number of versions for a GDG is 255.
- Each generation can have same or different DCB parameters.

**Why We Need GDG?**

- Record keeping
- Easy to relate data sets
- Auto deletion of outdated datasets
- No need to change the JCL every time.

**How to define a GDG?**

To use the GDG we have to define the GDG base / index.

```
//STEP10 EXEC PGM=IDCAMS
//SYSPRINT DD SYSOUT=*
//SYSIN DD *
            DEFINE GDG(NAME(TESTGDG.DATA.GDG) –
            LIMIT(10) –
            NOEMPTY –
            SCRATCH) 
/*
```

Where,
- GDG name can range from 1-44
- LIMIT can range from 1-255

**Empty Vs NoEmpty**

Empty:-This option will delete all the older generations if the limit of generations is reached

Example: If a GDG is defined with a limit of 10 and 11th generation is created then all the old 10 generations are deleted and the 11th generation is created.

NoEmpty:- This option will delete the oldest generation if the limit of generations is reached .

Example: If a GDG is defined with a limit of 10 and 11th generation is created then the 1st  generation is  deleted and the 11th generation is created.

**Scratch Vs NoScratch**

Scratch:- This option will delete the generation completely if the dataset is deleted. 

NoScratch :- This option will uncatalog the dataset if the dataset is deleted.

**Creating a GDG version**:
GDG version can be created in same JCL by giving +1 to the GDG base name.

```
STEP1   EXEC PGM=IEFBR14                                 
INFILE  DD  DSN= TESTGDG.DATA.GDG (+1),   
        DISP=(NEW,CATLG,DELETE),                         
        UNIT=SYSDA,                                      
        SPACE=(CYL,(200,200),RLSE),                      
       DCB=(LRECL=2700,BLKSIZE=0,RECFM=FB)                
```

**Altering a GDG**:

We can also change the attributes of a GDG using the ALTER keyword.

```
//STEP1   EXEC PGM=IDCAMS                      
//SYSPRINT DD SYSOUT=*                         
//SYSIN    DD *                                
    ALTER TESTGDG.DATA.GDG  NOSCRATCH     
/*      
```

**Deleting a GDG generation**:

```
//STEP1   EXEC PGM=IEFBR14                    
//DL       DD  DSN=TESTGDG.DATA.GDG(+1),      
//         DISP=(OLD,DELETE,DELTE)            
/*
```

**Deleting a GDG base /Index**:

Two parameters for deleting the base.

1.PURGE: Object will be deleted regardless of the expiration date. 

```
//SYSIN    DD  *                  
   DELETE TESTGDG.DATA.GDG PURGE    
```

2.FORCE:  Object will be delete even though it is not empty.   

```
//SYSIN    DD  *                  
   DELETE TESTGDG.DATA.GDG FORCE
```   
