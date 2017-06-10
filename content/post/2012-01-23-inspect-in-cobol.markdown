---
categories:
- Mainframe
- COBOL
date: 2012-01-23T10:40:00Z
date_gmt: 2012-01-23 10:40:00 +0530
published: true
status: publish
title: INSPECT in COBOL
---

The INSPECT verb has two options, TALLYING and REPLACING. You can do  one or the other or both. If both are done, the TALLYING IS DONE BEFORE  THE replacing. Some versions of the INSPECT require that all the  literals be in quotes. This may call for a redefination if the field is  numeric.

In using the TALLYING format of the INSPECT, you are tallying into a  field that is a counter. This field must be initialized to 0 before the  inspect is done. Unsually this is done by a MOVE 0 to whatever the  counter is called.

The TALLYING option of the INSPECT has multiple options - in fact, some  versions have options beyond those required by the COBOL specifications:

- You can tally ALL of something
- You can tally just the LEADING occurances of something
- You can just tally CHARACTERS
- You can tally BEFORE or AFTER an INITIAL specified character

**Example #1**: 

This statement counts the number of occurrences of the digit 5 until the first space is encountered. If FLDA = "256545 67" then after the INSPECT, CTRA would equal 3.

```
MOVE 0 TO CTRA.
NSPECT FLDA TALLY CTRA 
   FOR ALL "5" BEFORE INTIAL SPACE.
```

**Example #2**:

This statement counts the number of spaces in the field FLDB. If FLB = "4 5 6 1 2" then after the INSPECT, CTRB would equal 4 since there is a space between each number.

```
MOVE 0 TO CTRB.
INSPECT FLDB TALLYING CTRB<
   FOR ALL SPACES.
```

**Example #3**: 
In this example, the count of all characters before the first space is tallied. If FLDC is equal to 16AB5 6 then CTRC will contain the number 5 since 1, 6, A, B, and 5 proceed the space before the 6. 

```
MOVE 0 TO CTRC.
INSPECT FLDC TALLYING CTRC
    FOR CHARACTERS BEFORE INITIAL SPACE.
```

**Example #4**: 
This statement counts all of the leading zeros in a field. Embedded or trailing zeros are counted. IF FLDD is equal to 00090020, then CTRD is equal to 3.

```
MOVE 0 TO CTRD.
INSPECT FLDD TALLYING CTRD
    FOR LEADING ZEROS.
```

**Example #5**: This statement counts all zeros in the field. IF FLDE is equal to 00090020, then CTRE will be equal to 6.

```
MOVE 0 TO CTRE.
INSPECT FLDE TALLYING CTRE
    FOR ALL ZEROS.
```

**Example #6**: This statement tallies for all zeroes that proceed the initial 2 In this case, CTRF will be 5. FLDF is equal to 00090020.

```
INSPECT FLDF TALLYING CTRF
    FOR ALL ZEROS BEFORE INITIAL 2.
```

**Example #7**: This statement counts the spaces before the number 5. In this example CTRG will be 3. FLDG has three spaces and then the number 1257 ( 1257).

```
INSPECT FLDG TALLYING CTRG
    FOR LEADING SPACE BEFORE INITIAL 5.
```

**Example #8**: This statement will replace all B with G. FLDH will start as ABCBDFB and will become AGCGDFG.

```
INSPECT FLDH REPLACING ALL “B” BY “G”.
```

**Example #9**: This replace will change all A to X. This means that AAABBAAA will become XXXBBAAA.

```
INSPECT FLDI REPLACING CHARACTERS BY “X” 
    BEFORE INITIAL “B”.
```

**Example #10**: This will replace the first X with a 5. There ACXDGXB will become AC5DGXB.

```
INSPECT FLDJ REPLACING FIRST “X” BY “5”.
```
