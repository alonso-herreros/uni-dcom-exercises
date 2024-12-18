## Digital Communications <!-- omit in toc -->

# Chapter 3 Exercises

*Academic year 2024-2025*  

---

* [Exercise 1](#exercise-1)
    * [Question 1.1](#question-11)
    * [Question 1.2](#question-12)
* [Exercise 3](#exercise-3)
    * [Question 3.a)](#question-3a)
    * [Question 3.b)](#question-3b)
    * [Question 3.c)](#question-3c)
* [Exercise 4](#exercise-4)
    * [Question 4.c)](#question-4c)
    * [Question 4.d)](#question-4d)
* [Exercise 13](#exercise-13)
    * [Question 13.6](#question-136)

---

## Exercise 1

Consider to transmit a binary symbol constellation $\{1, +1\}$ through the
channel $p[n] = 0,5[n] 0,5[n - 1] + 0,8[n - 2]$.

### Question 1.1

Draw the trellis diagram labeling each branch with the corresponding metric.

```mermaid
%%{init: {'forceLegacyMathML':'true'} }%%
flowchart LR

subgraph s++ ["++"]
    s++1((" ")); s++2((" "))
end
subgraph s_+ ["-+"]
    s_+1((" ")); s_+2((" "))
end
subgraph s+_ ["+-"]
    s+_1((" ")); s+_2((" "))
end
subgraph s__ ["--"]
    s__1((" ")); s__2((" "))
end

s++1 --" 1 | 0.8"--> s++2
s++1 --"-1 | -0.2"--> s_+2

s_+1 --" 1 | 1.8"--> s+_2
s_+1 --"-1 | 0.8"--> s__2

s+_1 --" 1 | -0.8"--> s++2
s+_1 --"-1 | -1.8"--> s_+2

s__1 --" 1 | 0.2"--> s+_2
s__1 --"-1 | -0.8"--> s__2
```

Now, to find the minimum distance. Let's choose all 1's as our reference
sequence.

```mermaid
%%{init: {'forceLegacyMathML':'true'} }%%
flowchart LR

subgraph s++ ["++"]
    s++1((" ")) --> s++2((" ")) --> s++3((" ")) --> s++4((" ")) --> s++5((" "))
end
subgraph s_+ ["-+"]
    s_+1((" ")) ~~~ s_+2((" ")) ~~~ s_+3((" ")) ~~~ s_+4((" "))
end
subgraph s+_ ["+-"]
    s+_1((" ")) ~~~ s+_2((" ")) ~~~ s+_3((" ")) ~~~ s+_4((" "))
end
subgraph s__ ["--"]
    s__1((" ")) ~~~ s__2((" ")) ~~~ s__3((" ")) ~~~ s__4((" "))
end

s++1 --" 1 | d=1" --> s_+2(("1"))
s_+2 --" 1 | d=1" --> s+_3(("2"))
s+_3 --" 1 | d=2.56" --> s++4(("4.56"))
s_+2 --"-1 | d=0" --> s__3(("1"))
s+_3 --" 1 | d=0.36²" --> s+_4(("4.56"))
```

The only path back into the reference line goes through the `+-` node, and the
cost to get back is $2.56$. Since all other paths will have to use this link at some point, if their cost is higher than $4.56 - 2.56 = 2$, we can discard them.

The final node has a cost of $3.92$. Note that $D_{min}$ is the square root of
this value:

$$
D_{min} = \sqrt{3.92} = 1.98
$$

### Question 1.2

Determine the minimum distance Dmin.

## Exercise 3

A 4-PSK constellation, with equiprobable symbols $A[n] \in {+1, 1, +j, j}$ and
$E_s = 1$, is transmitted through the following equivalent discrete channel

$$
p[n] = [n] + j0.8[n - 1]
$$

with additive Gaussian white noise. The goal is to evaluate the performance of
the system with di↵erent receivers.

### Question 3.a)
If in the receiver there is a memoryless symbol by symbol detector

#### Section 3.a.i)

Obtain the received constellation without noise in the channel.

> **Answer**

| $A[n]$ | $A[n-1]$ | $o[n] = A[n] + j 0.8 A[n-1]$ |
| :----: | :------: | ---------------------------- |
| $1$    | $1$      | $1+j0.8$                     |
| $1$    | $-1$     | $1-j0.8$                     |
| $1$    | $j$      | $1-0.8 = 0.2$                |
| $1$    | $-j$     | $1+0.8 = 1.8$                |
| $-1$   | $1$      | $-1+j0.8$                    |
| $-1$   | $-1$     | $-1-j0.8$                    |
| $-1$   | $j$      | $-1-0.8 = -1.8$              |
| $-1$   | $-j$     | $-1+0.8 = -0.2$              |
| $j$    | $1$      | $j+j0.8 = 1.8j$              |
| $j$    | $-1$     | $j-j0.8 = 0.2j$              |
| $j$    | $j$      | $j-0.8 = -0.8 + j$           |
| $j$    | $-j$     | $j+0.8 = 0.8 + j$            |
| $-j$   | $1$      | $-j+j0.8 = 0.2j$             |
| $-j$   | $-1$     | $-j-j0.8 = -1.8j$            |
| $-j$   | $j$      | $-j-0.8 = 0.8 - j$           |
| $-j$   | $-j$     | $-j+0.8 = -0.8 - j$          |

#### Section 3.a.ii)

Calculate the probability of error Pe.

> **Answer**
>
> 0.28

The symbol-by-symbol detector will decide on distance, since the noise is white

### Question 3.b)
If the receiver is composed by a linear equalizer using the ZF criterion (without constrains in its complexity) and then a symbol by symbol detector

#### Section 3.b.i)

Obtain the transfer function of the equalizer.

#### Section 3.b.ii)

Estimate Pe.

### Question 3.c)
If the receiver is a ML (maximum likelihood) detector of sequences:

#### Section 3.c.i)

Obtain the trellis diagram and the minimum distance to an erroneous event.

#### Section 3.c.ii)

Obtain Pe and compare with the probabilities of error previously obtained.

## Exercise 4

### Question 4.c)

> **Answer**
>
> $$D_{min} = 0.79$$

### Question 4.d)

Decode the following sequence

$$
\bar{q} = \{0.2, -0.3, -0.3, 0.75\}
$$

using a a ML detector. Assume that $A[n] = 0$ for $n < 0$ and $n ≥ 3$

> **Answer**

```mermaid
%%{init: {'forceLegacyMathML':'true'} }%%
flowchart LR

subgraph s+ ["+1"]
    direction LR
    s+1((" ")); s+2((" "))
end
subgraph s0 ["0"]
    direction LR
    s01((" ")); s02((" "))
end
subgraph s- ["-1"]
    direction LR
    s-1((" ")); s-2((" "))
end

s-1 --"-1 | -0.5"--> s-2
s-1 --" 0 | 0.25"--> s02
s-1 --"+1 |   +1"--> s+2

s01 --"-1 | -0.75"--> s-2
s01 --" 0 |     0"--> s02
s01 --"+1 |  0.75"--> s+2

s+1 --"-1 |    -1"--> s-2
s+1 --" 0 | -0.25"--> s02
s+1 --"+1 |   0.5"--> s+2
```

Now we can build the trellis diagram for the sequence

```mermaid
%%{init: {'forceLegacyMathML':'true'} }%%
flowchart LR

subgraph s- [" "]
    direction LR
    s-1(["[-1]"]) ~~~ s-2((" ")); s-3((" ")); s-4((" ")) ~~~ s-5((" "))
end
subgraph s0 [" "]
    direction LR
    s01(["[0]"]); s02((" ")); s03((" ")); s04((" ")); s05((" "))
end
subgraph s+ [" "]
    direction LR
    s+1(["[+1]"]) ~~~ s+2((" ")); s+3((" ")); s+4((" ")) ~~~ s+5((" "))
end

s01 --"(0.2- (-0.75))²=0.9"--> s-2
s01 =="(0.2-0)²=0.04"      ==> s02
s01 --"(0.2-0.75)²=0.3"    --> s+2

s-2((0.9))
s02((0.04))
s+2((0.3))

s-2 -."0.04" .->s-3
s-2 -."0.3"  .->s03
s-2 -."1.69" .->s+3
s02 =="0.2"  ==>s-3
s02 --"0.09" -->s03
s02 -."1.1"  .->s+3
s+2 -."0.49" .->s-3
s+2 -."0.002".->s03
s+2 --"0.64" -->s+3

s-3((0.24))
s03((0.13))
s+3((0.94))

s-3 =="0.04" ==>s-4
s-3 -."0.3"  .->s04
s-3 -."1.69" .->s+4
s03 -."0.2"  .->s-4
s03 --"0.09" -->s04
s03 --"1.1"  -->s+4
s+3 -."0.49" .->s-4
s+3 -."0.002".->s04
s+3 -."0.64" .->s+4

s-4((0.28))
s04((0.22))
s+4((1.23))

s-4 =="0.25" ==>s05
s04 -."0.56" .->s05
s+4 -."1"    .->s05 

s05((0.53))

```

## Exercise 13

$$
p[n] = 0.5 δ[n] + δ[n-1] + 0,5 δ[n-2]
$$

$$
A[n] = ±1
$$

### Question 13.6

$$
A[-2], A[-1], A[3], A[4] = 1, 1, 1, 1
$$

$$
\bar{q} = \{1.6, 0.2, 0, -0.1, 1.3\}
$$

> **Answer**

Transitions:

```mermaid
%%{init: {'forceLegacyMathML':'true'} }%%
flowchart LR

subgraph s++ [" "]
    s++1(["[+1, +1]"]); s++2((" "))
end
subgraph s_+ [" "]
    s_+1(["[-1, +1]"]); s_+2((" "))
end
subgraph s+_ [" "]
    s+_1(["[+1, -1]"]); s+_2((" "))
end
subgraph s__ [" "]
    s__1(["[-1, -1]"]); s__2((" "))
end

s++1 --" 1 |  2"--> s++2
s++1 --"-1 |  1"--> s_+2
s_+1 --" 1 |  0"--> s+_2
s_+1 --"-1 | -1"--> s__2
s+_1 --" 1 |  1"--> s++2
s+_1 --"-1 |  0"--> s_+2
s__1 --" 1 | -1"--> s+_2
s__1 --"-1 | -2"--> s__2 
```

Sequence:

```mermaid
%%{init: {'forceLegacyMathML':'true'} }%%
flowchart LR

subgraph s++ [" "]
    direction LR
    s++1(["[+1,+1]"]); s++2((" ")); s++3((" ")); s++4((" ")); s++5((" ")); s++6([" "])
end
subgraph s_+ [" "]
    direction LR
    s_+1(["[-1,+1]"]); s_+2((" ")); s_+3((" ")); s_+4((" ")); s_+5((" ")); s_+6((" "))
end
subgraph s+_ [" "]
    direction LR
    s+_1(["[+1,-1]"]); s+_2((" ")); s+_3((" ")); s+_4((" ")); s+_5((" ")); s+_6((" "))
end
subgraph s__ [" "]
    direction LR
    s__1(["[-1,-1]"]); s__2((" ")); s__3((" ")); s__4((" ")); s__5((" ")); s__6((" "))
end

s++1 --"(1.6-2)²=0.16"--> s++2
s++1 =="(1.6-1)²=0.36"==> s_+2
s_+1 ~~~ s_+2
s+_1 ~~~ s+_2
s__1 ~~~ s__2

s++2(("0.16"))
s_+2(("0.36"))
s+_2((" "))
s__2((" "))

s++2 --"3.24 "--> s++3
s++2 --"0.64 "--> s_+3
s_+2 =="0.04 "==> s+_3
s_+2 --"1.44 "--> s__3
s+_2 ~~~ s++3
s__2 ~~~ s+_3
s++3(("3.4"))
s_+3(("0.8"))
s+_3(("0.4"))
s__3(("1.8"))


s++3 -."4    ".->s++4
s++3 -."1    ".->s_+4
s_+3 --"0    "-->s+_4
s_+3 --"2    "-->s__4
s+_3 =="1    "==>s++4
s+_3 --"0    "-->s_+4
s__3 -."1    ".->s+_4
s__3 -."4    ".->s__4
s++4(("1.4"))
s_+4(("0.4"))
s+_4(("0.8"))
s__4(("1.8"))


s++4 -."4.41 ".->s++5
s++4 =="0.01 "==>s+_5
s+_4 --"1.21 "-->s++5
s__4 -."0.81 ".->s+_5
s_+4 ~~~ s_+5
s__4 ~~~ s__5
s++5(("2.01"))
%% s_+5((" "))
s+_5(("0.41"))
%% s__5((" "))


s++5 -."0.49 ".->s++6
s+_5 =="0.09 "==>s++6
s+_5 ~~~ s+_6
s_+5 ~~~ s_+6
s__5 ~~~ s__6
s++6(["0.5"])
s_+6((" "))
s+_6((" "))
s__6((" "))
```
