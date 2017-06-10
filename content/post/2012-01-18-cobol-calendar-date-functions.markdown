---
categories:
- COBOL
comments: []
date: 2012-01-18T17:49:00Z
date_gmt: 2012-01-18 17:49:00 +0530
published: true
status: publish
title: COBOL Calendar and Date Functions
---

You need to know what date is 150 days from today (and this kind of stuff happens more often than you'd think)? Convert today to an integer date, add 150 to it and convert it back. No more checking which months you're going through to see if it's a 30 day or 31 day month. No more leap year calculations.

**Some sample COBOL Date Example:**

{{< highlight cobol >}}
01  WS-TODAY         PIC 9(8).
01  WS-FUTURE-DATE   PIC 9(8).
....
MOVE FUNCTION CURRENT-DATE (1:8) TO WS-TODAY.
COMPUTE WS-FUTURE-DATE = FUNCTION INTEGER-OF-DATE (WS-TODAY) + 150
{{< / highlight >}}

Probably the most useful intrinsic function is **CURRENT-DATE** which is a replacement for ACCEPT DATE and ACCEPT TIME. CURRENT-DATE is Y2K-compliant, having a 4-digit year. This function returns a 20-character alphanumeric field which is laid out as follows:

{{< highlight cobol >}}
01  WS-CURRENT-DATE-FIELDS.
05  WS-CURRENT-DATE.
10  WS-CURRENT-YEAR    PIC  9(4).
10  WS-CURRENT-MONTH   PIC  9(2).
10  WS-CURRENT-DAY     PIC  9(2).
05  WS-CURRENT-TIME.
10  WS-CURRENT-HOUR    PIC  9(2).
10  WS-CURRENT-MINUTE  PIC  9(2).
10  WS-CURRENT-SECOND  PIC  9(2).
10  WS-CURRENT-MS      PIC  9(2).
05  WS-DIFF-FROM-GMT       PIC S9(4).
{{< / highlight >}}

So not only can you get the time down to the millisecond, but you can get the difference between your time and Greenwich Mean Time.

The function is used in a MOVE:

{{< highlight cobol >}}
MOVE FUNCTION CURRENT-DATE TO WS-CURRENT-DATE-FIELDS
{{< / highlight >}}

The other intrinsic date functions deal with converting between either Gregorian dates or Julian dates and an internal Integer format. This Integer format is simply the number of days since some predetermined, fixed date like 1/1/0001. These four conversion functions are:

### Convert from Gregorian to Integer formats

{{< highlight cobol >}}
COMPUTE WS-INTEGER-DATE = FUNCTION INTEGER-OF-DATE (WS-DATE)
{{< / highlight >}}

### Convert from Integer to Gregorian formats

{{< highlight cobol >}}
COMPUTE WS-DATE = FUNCTION DATE-OF-INTEGER (WS-INT-DATE)
{{< / highlight >}}

### Convert from Julian to Integer formats

{{< highlight cobol >}}
COMPUTE WS-INTEGER-DATE = FUNCTION INTEGER-OF-DAY (WS-JUL-DATE)
{{< / highlight >}}

### Convert from Integer to Julian formats

{{< highlight cobol >}}
COMPUTE WS-JULIAN-DATE = FUNCTION DAY-OF-INTEGER (WS-INT-DATE)
{{< / highlight >}}

- All Gregorian and Julian dates are expected to have 4-digit years.

- COMPUTE is OK because we're only using integers here.

### How many days between two dates?

{{< highlight cobol >}}
COMPUTE WS-DAYS = FUNCTION INTEGER-OF-DATE (WS-DATE-1) - 
                        FUNCTION INTEGER-OF-DATE (WS-DATE-2)
{{< / highlight >}}

### Converting between Gregorian and Julian formats used to be a pain also. Now it's easy as below.

{{< highlight cobol >}}
COMPUTE WS-DATE = FUNCTION DATE-OF-INTEGER (FUNCTION INTEGER-OF-DAY (WS-JULIAN))
{{< / highlight >}}
