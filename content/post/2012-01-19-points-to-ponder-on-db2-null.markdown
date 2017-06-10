---
categories:
- Mainframe
- DB2
date: 2012-01-19T21:40:00Z
date_gmt: 2012-01-19 21:40:00 +0530
published: true
status: publish
title: Points to Ponder on DB2 NULL
---

- NULLs can present problems because they are handled differently by different computers and the collating sequence is inconsistent with regard to NULLs.
- Unless you specify NOT NULL, the default is to allow for NULLs.
- It's easy for us to get lazy and allow columns to contain NULLs when it would be better to specify NOT NULL. Allowing for NULLs will create UNKNOWN logical values. Always test your code with NULLs in all possible places.
- The NULL is a global creature, not belonging to any particular data type, but able to replace any of their values.
- A NULL isn't a zero, it isn't a blank string, it isn't a string of length zero.
- The basic rule for math with NULLs is that they propagate. An arithmetic operation with a NULL will return a NULL. If you have a NULL in an expression, the result will be NULL.
- If you concatenate a zero length string to another string, that string stays the same. If you concatenate a NULL string to a string, the string becomes a NULL.
- In comparisons, the results can be TRUE, FALSE, or UNKNOWN. A NULL in a row will give an UNKNOWN result in the comparison.
- Sometimes negating the wording of the problem helps. Instead of saying "Give me the cars that met all the test criteria," say "Don't give me any car that failed one of the test criteria." It is often easier to find what you do not want than what you do want. This is very true when you use the NOT EXISTS, but beware of NULLs and empty tables when you try this.
- You can't completely avoid NULLs in SQL. However, it is a good idea to try as hard as you can to avoid them whenever possible.
- Make yourself think about whether you really need NULLs to exist in a column before you omit the NOT NULL clause on the column definition.
- Use NULLs sparingly.

**Source:** Unkown
