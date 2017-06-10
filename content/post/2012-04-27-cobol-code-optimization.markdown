---
categories:
- Mainframe
- COBOL
date: 2012-04-27T10:08:00Z
date_gmt: 2012-04-27 04:38:00 +0530
published: true
status: publish
title: COBOL Code Optimization
---

To assist in the optimization of the code, you should use the OPTIMIZE compiler option. With the OPTIMIZE(STD) or OPTIMIZE(FULL) options in effect, you may receive optimizations that include:

- eliminating unnecessary branches
- simplifying inefficient branches
- simplifying the code for the out-of-line PERFORM statement, moving the performed paragraphs in-line,where possible
- simplifying the code for a CALL to a contained (nested) program, moving the called statements in-line,where possible
- eliminating duplicate computations
- eliminating constant computations
- aggregating moves of contiguous, equal-sized items into a single move
- deleting unreachable code

Additionally, with the OPTIMIZE(FULL) option in effect, you may also receive these optimizations:

- deleting unreferenced data items and the associated code to initialize their VALUE clauses

Many of these optimizations are not available with OS/VS COBOL, but are available with IBM Enterprise COBOL. NOOPTIMIZE is generally used while a program is being developed when frequent compiles are necessary.
 
NOOPTIMIZE can make it easier to debug a program since code is not moved. However, IBM Enterprise COBOL now supports debugging programs compiled with the OPTIMIZE compiler option.

OPTIMIZE requires more CPU time for compiles than NOOPTIMIZE, but generally produces more
efficient run-time code. For production runs, OPTIMIZE is recommended.

> WARNING: If your program relies upon unreferenced level 01 or level 77 data items, you should not use OPTIMIZE(FULL), since OPTIMIZE(FULL) will delete all unreferenced data items. One way to prevent the data item from being deleted by the OPTIMIZE(FULL) option is to refer to the data item in the PROCEDURE DIVISION (for example, initialize the data item with a PROCEDURE DIVISION statement instead of with VALUE clauses).

**Performance considerations using OPTIMIZE**:

On the average, OPTIMIZE(STD) was 1% faster than NOOPTIMIZE, with a range of 7% faster to equivalent.
On the average, OPTIMIZE(FULL) was equivalent to OPTIMIZE(STD).
