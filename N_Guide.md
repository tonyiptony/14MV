#  Logic Guide to [N]egation

*Written by: T.KAZ3-1#2745*

*Draft 1: 28 Jan 2023*

### *Negation: the clue indiates the difference in the number of mines between colored and uncolored cells.*

**Reminder: If you are stuck, always start by clicking on every clue first!**

## Introduction

Like other checkerboard coloring variants, [N]egation is mostly about parity comparison. You'll be asking whether a group of cells' *difference* (in the number of mines) is:
- **odd/even**?
- **net zero**?
- **dark/white up one**?

etc.

[N] requires quite a bit of pencilmark work and case checks. End game counting often required.

## Terminology

- [ , ] is the rectangular group of cells from top left to bottom right. e.g. [B1,C2] will consists of B1, B2, C1, C2.
- The **group difference** of two groups is the the difference of cells from the bigger group take away the smaller group. e.g. The group difference of [B1,C2] and [B1,B2] is [C1,C2].
- [ , ] is **odd/even** if the difference in the number of mines is odd/even. e.g. [B1,C2] is odd if it has "1 dark 0 light" or "0 dark 1 light".
- [ , ] is **net zero** if the difference in dark/light mines is zero. e.g. [B1,C2] is net zero if it has "0 dark 0 light" or "1 dark 1 light".
- [ , ] is **dark/light up one** if there are exactly one more dark/light mine than the other. e.g. [B1,C2] is dark up one if it has "1 dark 0 light" or "2 dark 1 light".
    - Sometimes we skip the coloring descriptor if we don't know which color is up.



It is also implied that if a group is **dark up two**, then it's **up two**, and then it's **even**.
(From most detailed knowledge gained to most general)

## Basic logic - Parity checks

It is often easier to check clues on the edge first, as they are easy group difference parity checks.

### TL;DR on group difference logic
The group difference of:
1. Odd & even groups is odd
2. Odd & odd groups, even & even groups is even
3. Net zero & net zero groups is net zero
4. Net zero & up one groups is up one.
5. Dark up one & net zero groups is light up one.

### Example 1: Odd & even

Let's look at [F6,H8]. We see consecutive clues in G7 and H7. So a parity check looks like this:
1. H7 is 1 $\implies$ [G6,H8] is odd.
2. G7 is 0 $\implies$ [F6,H8] is even.
3. The group difference, [F6,F8], is thus odd.
4. F6 must be the mine!

![Example 1.gif](https://raw.githubusercontent.com/tonyiptony/14MV/main/gifs/Parity/N_Basic.gif)

### Example 2: Odd and odd

Similarly, let's look at [A6,C8]. Again, consecutive 1s in A7 and B7, so parity check time:
1. A7 is 1 $\implies$ [A6,B8] is odd.
2. B7 is 1 $\implies$ [A6,C8] is odd.
3. The group difference, [C6,C8], is thus even.
4. C6 must be the mine!

![Example 2.gif](https://raw.githubusercontent.com/tonyiptony/14MV/main/gifs/Net%20zero_1/ezgif-3-5bcb430375.gif)

#### *Warning on even group difference*
While we do know the group difference is even, we don't know if the difference is 0 or 2! It is often a trap you will run into.

### Example 3: Cascade

The power of parity checks is they often infer other neighboring groups as well. Let's see [A1,A5]:
1. A1 is 0 $\implies$ [A1,B2] is net zero.
2. A2 is 0 $\implies$ [A1,B3] is net zero.
3. The group difference, [A3,B3], is thus net zero.
4. A4 is 2 $\implies$ [A3, B5] is up two.
5. The group difference, [A4, B5], is thus up two.
6. B4, A5 must be the mines, and B5 is safe!

![Example 3.gif](https://raw.githubusercontent.com/tonyiptony/14MV/main/gifs/Parity%2B/ezgif-3-b379f5e4d8.gif)

### Example 4: Corner

Let's see [A6,C8]:
1. A7 is 0 $\implies$ [A6,B8] is net zero.
2. B7 is 1 $\implies$ [A6,C8] is up one.
3. The group differeence, [C6,C8], is thus up one.
4. B8 is 0 $\implies$ [A7,C8] is net zero $\implies$ [C7,C8] is net zero.
5. The group difference, C6, is thus up one, i.e. the mine!

![Example 4.gif](https://raw.githubusercontent.com/tonyiptony/14MV/main/gifs/4_Corner/ezgif-3-1fc454fa78.gif)

### Example 5 - Color difference
Similar to Example 4, this time we add in coloring considerations. Let's see [A2,C4]:
1. A3 is 1 $\implies$ [A2,B4] is odd.
2. B2 is a known mine $\implies$ [A2,B2] is odd.
3. The group difference, [A3,B4], is thus even.
4. We must have [A4,B4] being net zero, as it can't be up 2.
5. Combining with the known mine in B2, we have [A2,B4] being **dark** up one (better knowledge than just odd now).
6. Together with B3 is 0 $\implies$ [A2,C5] is net zero, we know the group difference [C3,C4] is **light** up one.
7. C4 is the mine and C3 is safe!

![Example 5.gif](https://raw.githubusercontent.com/tonyiptony/14MV/main/gifs/5_Color%20diff/ezgif-3-5e82f7fec8.gif)

## End game counting
A lot of [N] puzzles require looking at the remaining mine count. It goes along with parity checks.
Let's look at [F5,H7], we have 7 remaining mines to fill in 8 blank spaces:
1. G6 is 2 $\implies$ [F5,H7] is up two $\implies$ [F5,H5] is net zero.
2. Net zero in 3 blank spaces has either 0 mines or 2 mines (one dark one light)
3. But we can't have 0 mines, or else we need to fill in 7 mines in 5 spaces! Thus we need 2 mines.
4. That means, we need one dark mine and one light mine. The dark mine is confirmed!

We can then complete the puzzle by considering [E3,G5] and the 1 in F4, again by end game counting. Do you see that [E5,F5] is net zero?

![End game.gif](https://raw.githubusercontent.com/tonyiptony/14MV/main/gifs/End%20game/ezgif-3-5cd4933e74.gif)


```python

```
