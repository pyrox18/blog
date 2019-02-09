---
layout: post
title: BMAT Brain Teaser: Finding the last digit of a 6-digit PIN
tags: bmat pin banking unique
---

Recently, a friend of mine asked for some pointers on an examination problem that his sister was trying to solve. It went something like this:

> My 6-digit passcode for internet banking consists of six different digits. The second digit is 8. When the passcode is written as three 2-digit numbers, the three numbers add up to 80. When it is written as two 3-digit numbers, the two numbers add up to 800. What is the last digit of my passcode?

This question is from a past year paper of the BioMedical Admissions Test (BMAT), a test used in the admission process for medical courses in some universities. I'm not sure why anyone would design an internet banking system with a passcode that only consists of 6 unique digits, but let's just get on with the solution.

## Setting up

For starters, let's divide the passcode into its six characters, with each character represented by the letters `a` through `f`:

```
+-+-+-+-+-+-+
|a|b|c|d|e|f|
+-+-+-+-+-+-+
```

Our objective here is to try and find the value of `f`. From the question, we know that the second digit of the passcode is 8, i.e. `b = 8`. Thus, our passcode now looks like this:

```
+-+-+-+-+-+-+
|a|8|c|d|e|f|
+-+-+-+-+-+-+
```

Then, we have this line:

> When the passcode is written as three 2-digit numbers, the three numbers add up to 80.

We can represent this addition equation as something like this:

```
  a b
  c d
+ e f
  ---
  8 0
  ===
```

Substituting `b = 8`, we get:

```
  a 8
  c d
+ e f
  ---
  8 0
  ===
```

We'll get back to this equation later. For now, let's look at the next part of the question:

> When it is written as two 3-digit numbers, the two numbers add up to 800. 

Similar to the previous equation, this part of the question can be represented as follows:

```
  a b c
+ d e f
  -----
  8 0 0
  =====
```

Once again, substituting `b = 8`, we get:

```
  a 8 c
+ d e f
  -----
  8 0 0
  =====
```

## Deriving equations from the three-digit groups

We'll start working our way forward using the three-digit groups. Here, we can notice that for the result of a certain column to be a 0, the sum of the augend and addend (in plain English: the two numbers being added together) must be a multiple of 10 (i.e. 0, 10, 20, ...). In the equation above, this means that

```
c + f = 0 or 10 or 20 or ...
```

However, the range of these multiples of 10 can be limited due to the following factors.

- The largest possible number that can be attained by adding two unique non-negative single-digit numbers together is 17 (`8 + 9`), meaning that any multiple of 10 higher than 17 is not obtainable.
- To obtain a sum of 0, `c` and `f` must both be 0 (i.e. `0 + 0 = 0`). However, since each digit in the passcode is supposed to be unique, this is impossible.

This leaves us with 10 being the only possible sum for each column that has a result of 0.

Now we know that

```
c + f = 10
```

We then carry the `1` to the next column. We obtain the following equation:

```
1 (carry) + 8 + e = 10
```

Here, we can easily derive the value of `e`.

```
1 (carry) + 8 + e = 10
                e = 10 - 8 - 1
                e = 1
```

There is also a carry digit here (`1`) to be taken to the next column. We then arrive at the following equation:

```
1 (carry) + a + d = 8
            a + d = 8 - 1
            a + d = 7
```

We're done deriving equations with the three-digit groups, so let's think back about our objective. We're trying to look for the last digit in the passcode, which we represent here as `f`. So let's tabulate all the possible values for the `c` and `f` pair in the first column, since we know that those two digits have to add up to 10.

|c|f|
|---|---|
|1|9|
|2|8|
|3|7|
|4|6|
|5|5|
|6|4|
|7|3|
|8|2|
|9|1|

We know that the digits `8` and `1` are being used by `b` and `e` respectively, so neither `c` nor `f` can possess these digits. We also know that the digits are unique, so `c` and `f` cannot possess the value `5` at the same time. Therefore, we are left with the following possibilities:

|c|f|
|---|---|
|3|7|
|4|6|
|6|4|
|7|3|

## Switching back to the two-digit groups

We can't go any further with the three-digit groups, so let's go back and take a look at the set of two-digit groups:

```
  a 8
  c d
+ e f
  ---
  8 0
  ===
```

Earlier, we have found that `e = 1`, so let's substitute that in:

```
  a 8
  c d
+ 1 f
  ---
  8 0
  ===
```

From here on, we can attempt to substitute all possible values of `c` and `f` to find a solution.

Notice that the columns with a result of 0 here can have the sum of the column's augends and addends be either 10 or 20, since the largest possible value that can be obtained by adding three non-negative single-digit numbers together is 24 (`9 + 8 + 7`).


## Possibility 1: (c, f) = (7, 3)

```
  a 8
  7 d
+ 1 3
  ---
  8 0
  ===
```

`8 + d + 3 > 10`; therefore:

```
8 + d + 3 = 20
        d = 20 - 8 - 3
        d = 9
```

We know that `a + d = 7`, so:

```
a + 9 = 7
    a = 7 - 9
    a = -2
```

This is invalid as the digits are supposed to be non-negative. Therefore, `(c, f) != (7, 3)`.

## Possibility 2: (c, f) = (6, 4)

```
  a 8
  6 d
+ 1 4
  ---
  8 0
  ===
```

`8 + d + 4 > 10`; therefore:

```
8 + d + 4 = 20
        d = 20 - 8 - 4
        d = 8
```

However, the digit `8` is already used by `b`. Therefore, `(c, f) != (6, 4)`.

## Possibility 3: (c, f) = (4, 6)

```
  a 8
  4 d
+ 1 6
  ---
  8 0
  ===
```

`8 + d + 6 > 10`; therefore:

```
8 + d + 6 = 20
        d = 20 - 8 - 6
        d = 6
```

However, the digit `6` is already used by `f`. Therefore, `(c, f) != (4, 6)`.

## Possibility 4: (c, f) = (3, 7)

```
  a 8
  3 d
+ 1 7
  ---
  8 0
  ===
```

`8 + d + 7 > 10`; therefore:

```
8 + d + 7 = 20
        d = 20 - 8 - 7
        d = 5
```

We know that `a + d = 7`, so:

```
a + 5 = 7
    a = 7 - 5
    a = 2
```

Then, adding the numbers in the left column:

```
2 (carry) + a + 3 + 1
= 2 + 2 + 3 + 1
= 8
```

Since the equations are valid, we can determine that `(c, f) = (3, 7)`.

## Result

From the derivations made above, the full passcode can be determined as follows:

```
+-+-+-+-+-+-+
|a|b|c|d|e|f|
+-+-+-+-+-+-+
|2|8|3|5|1|7|
+-+-+-+-+-+-+
```

The last digit is, therefore, `7`.

## References

- https://www.thestudentroom.co.uk/showthread.php?t=4873140&page=2