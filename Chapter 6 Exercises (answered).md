## Digital Communications <!-- omit in toc -->

# Chapter 6 Exercises

*Academic year 2024-2025*  

<!--
$$
\global\def\BBar#1{\overline{\overline{#1}}}
$$
I whish this worked when exported
-->

---

### Table of Contents

* [Exercise 1 ✓](#exercise-1-)
* [Exercise 5.a)](#exercise-5a)
    * [Question 5.1.i) ✓](#question-51i-)
    * [Question 5.a.ii)](#question-5aii)
* [Exercise 5.b)](#exercise-5b)
    * [Question 5.b.i) ✓](#question-5bi-)
    * [Question 5.b.ii) ✓](#question-5bii-)
    * [Question 5.b.iii)](#question-5biii)
    * [Question 5.b.iv) ✓](#question-5biv-)

---

## Exercise 1 ✓

The encoding matrix for a linear block code $(4, 8)$ is given next. Compute the
coding rate, the minimum distance and the syndrome table.

$$
\def\BBar#1{\overline{\overline{#1}}}
\BBar{G} = \begin{bmatrix}
    1 & 1 & 1 & 1 & 1 & 1 & 1 & 1 \\
    0 & 1 & 1 & 1 & 0 & 0 & 1 & 0 \\
    0 & 0 & 1 & 1 & 1 & 0 & 0 & 1 \\
    0 & 0 & 0 & 1 & 0 & 1 & 1 & 1 \\
\end{bmatrix}
$$

> **Answer** (class notes)
>
> The coding rate is simply computed as
>
> $$
> \frac{k}{n} = \frac{4}{8} = \boxed{0.5}
> $$
>
> The basic way to compute the minimum distance is to compute the Hamming
> distance between all possible pairs of codewords.
>
> $$
> d_{\min} = \min_{i≠j} d_H(\bar{c}_i, \bar{c}_j)
> $$
>
> This is a very tedious process, so we will compare the rows of the generating
> matrix. By doing **6 comparisons**, we can see that no two rows differ by less
> than 4 bits, so the minimum distance is
>
> $$
> \boxed{d_{\min} = 4}
> $$
>
> Now, we will compute the syndrome table, which is computed by multiplying all
> possible error patterns by $\overline{\overline{H}}$, which is only easy to
> compute if we have a generating matrix of the form
>
> $$
> \def\BBar#1{\overline{\overline{#1}}}
> \BBar{G} = \begin{bmatrix}
>     \begin{array}{c:c}
>     \BBar{I}_{k} & \BBar{P} \\
>     \end{array}
> \end{bmatrix} \text{ or } \begin{bmatrix}
>     \begin{array}{c:c}
>     \BBar{P} & \BBar{I}_{k} \\
>     \end{array}
> \end{bmatrix}
> $$
>
> We will transform our matrix to this form by performing elementary row
> operations.
>
> $$
> \def\BBar#1{\overline{\overline{#1}}}
> \begin{aligned}
>     \BBar{G}' &= \begin{bmatrix}
>         \bar{g}_1 + \bar{g}_2 \\
>         \bar{g}_2 + \bar{g}_3 \\
>         \bar{g}_3 + \bar{g}_4 \\
>         \bar{g}_4 \\
>     \end{bmatrix} &= \begin{bmatrix}
>         1 & 0 & 0 & 0 & 1 & 1 & 0 & 1 \\
>         0 & 1 & 0 & 0 & 1 & 0 & 1 & 1 \\
>         0 & 0 & 1 & 0 & 1 & 1 & 1 & 0 \\
>         0 & 0 & 0 & 1 & 0 & 1 & 1 & 1 \\
>     \end{bmatrix}
> \end{aligned}
> $$
>
> If we add an identity to the bottom of the right part of our
> $\overline{\overline{G}'$ (which is the parity matrix
> $\overline{\overline{P}}$), we can directly obtain the transpose of the
> parity-check matrix, which we will use to compute the syndrome table.
>
> $$
> \def\BBar#1{\overline{\overline{#1}}}
> \BBar{H}^T = \begin{bmatrix}
>     1 & 1 & 0 & 1 \\
>     1 & 0 & 1 & 1 \\
>     1 & 1 & 1 & 0 \\
>     0 & 1 & 1 & 1 \\
>     1 & 0 & 0 & 0 \\
>     0 & 1 & 0 & 0 \\
>     0 & 0 & 1 & 0 \\
>     0 & 0 & 0 & 1 \\
> \end{bmatrix}
> $$
>
> Now, we will compute the syndrome table by multiplying possible error patterns
> by $\overline{\overline{H}}^T$. First, we'll add all the error patterns with 1
> bit flipped. After that, we'll first add all the syndromes that are left, and
> find the error patterns that produce them with the least number of bits
> flipped.
>
> | Error pattern $\bar{e}$ | Syndrome $\bar{s} = \bar{e} ⋅ \overline{\overline{H}}^T$ |
> | :---------------------: | :------------------------------------------------------: |
> |       `00000000`        |                          `0000`                          |
> |       `00000001`        |                          `0001`                          |
> |       `00000010`        |                          `0010`                          |
> |       `00000100`        |                          `0100`                          |
> |       `00001000`        |                          `1000`                          |
> |       `00010000`        |                          `0111`                          |
> |       `00100000`        |                          `1110`                          |
> |       `01000000`        |                          `1011`                          |
> |       `10000000`        |                          `1101`                          |
> |       `00000011`        |                          `0011`                          |
> |       `00000101`        |                          `0101`                          |
> |       `00000110`        |                          `0110`                          |
> |       `00001001`        |                          `1001`                          |
> |       `00001010`        |                          `1010`                          |
> |       `00001100`        |                          `1100`                          |
> |       `00100001`        |                          `1111`                          |
>
> > **Extra**
> >
> > Imagine you receive the word $\bar{r} = 00010011$. In order to decode it,
> > you have two options:
> >
> > 1. Compute the Hamming distance with all codewords and choose the one with
> > the minimum distance:
> >
> >     $$
> >     \hat{\bar{c}}_i = \arg\min_{\bar{c}_i} d_H(\bar{r}, \bar{c_i})
> >     $$
> >
> > 2. Much easier to do is finding the syndrome $\bar{s}$ and checking the
> > syndrome table, then flipping the corresponding bits.
> >
> >     $$
> >     \def\BBar#1{\overline{\overline{#1}}}
> >     \bar{s} = \bar{r} ⋅ \BBar{H}^T = 0100 \\
> >     $$
> >
> >     $$
> >     \begin{aligned}
> >         \hat{\bar{c}} &= \bar{r} + \bar{e} \\
> >         &= 00010011 ⊕ 00000100 \\
> >         &= 00010111
> >     \end{aligned}
> >     $$

## Exercise 5.a)
A linear block code has the following generating matrix

$$
\def\BBar#1{\overline{\overline{#1}}}
\BBar{G} = \begin{bmatrix}
    0 & 1 & a & 0 & b \\
    c & d & 1 & 1 & 1 \\
\end{bmatrix}
$$

### Question 5.a.i) ✓
Get $a$, $b$, $c$ and $d$ values to obtain the maximum detection and correction
capabilities.

> **Answer** (class notes)
>
> To maximize the detection and correction capabilities of a code, we need to
> **maximize the minimum distance** of the code. Let's get the codewords:
>
> $$
> \def\BBar#1{\overline{\overline{#1}}}
> \begin{aligned}
>     \bar{c}_i &= \bar{b}_i ⋅ \BBar{G} \\
>     \bar{c}_1 &= \bar{b}_1 ⋅ \BBar{G} &= [0\;0] ⋅ \BBar{G} &=& [0&,&   0&,&   0&,& 0&,&   0&] \\
>     \bar{c}_2 &= \bar{b}_2 ⋅ \BBar{G} &= [0\;1] ⋅ \BBar{G} &=& [c&,&   d&,&   1&,& 1&,&   1&] \\
>     \bar{c}_3 &= \bar{b}_3 ⋅ \BBar{G} &= [1\;0] ⋅ \BBar{G} &=& [0&,&   1&,&   a&,& 0&,&   b&] \\
>     \bar{c}_4 &= \bar{b}_4 ⋅ \BBar{G} &= [1\;1] ⋅ \BBar{G} &=& [c&,& 1⊕d&,& 1⊕a&,& 1&,& 1⊕b&] \\
> \end{aligned}
> $$
>
> The 6 distances are:
>
> $$
> \begin{aligned}
>     d_H(\bar{c}_1, \bar{c}_2) &= 3+c+d \\
>     d_H(\bar{c}_1, \bar{c}_3) &= 1+a+b \\
>     d_H(\bar{c}_1, \bar{c}_4) &= 4+c-d-a-b \\
>     d_H(\bar{c}_2, \bar{c}_3) &= 4+c-d-a-b \\
>     d_H(\bar{c}_2, \bar{c}_4) &= 1+a+b \\
>     d_H(\bar{c}_3, \bar{c}_4) &= 3+c+d \\
> \end{aligned}
> $$
>
> As we can see, not all distances are unique, so we could have only computed
> the distance between the first and all other codewords, skipping the rest.
> This may or may not be always the case.
>
> To maximize the minimum distance, let's start by maximizing what seems the
> most restrictive line:
>
> $$
> \begin{aligned}
>     \max_{a,b} d_H(\bar{c}_1, \bar{c}_3) &= \max_{a,b} \{1+a+b\} \\
>     &= 1+1+1 \\
>     &= 3 \\
>     % 1+a+b & ≥ 3 \\
> \end{aligned} \\
> a=b=1 \\
> $$
>
> The best minimum distance we can possibly get is 3, with the values of $a$ and
> $b$ we just found.
>
> This next line is just as restrictive. Let's try to make the distance equal 3
> as well:
>
> $$
> \begin{aligned}
>     d_H(\bar{c}_1, \bar{c}_4) &= 3 \\
>     4+c-d-a-b &= 3 \\
>     2+c-d &= 3 \\
>     c=1;\; d=0 \\
> \end{aligned}
> $$
>
> Finally, let's check if the last one holds
>
> $$
> \begin{aligned}
>     d_H(\bar{c}_1, \bar{c}_2) &≥ 3 \\
>     3+c+d &≥ 3 \\
>     4 &≥ 3 \\
> \end{aligned}
> $$
>
> With this, we have found our optimal values:
>
> $$
> \boxed{\begin{aligned}
>     a &= 1; & b &= 1 \\
>     c &= 1; & d &= 0 \\
> \end{aligned}}
> $$
>
> $$
> \def\BBar#1{\overline{\overline{#1}}}
> \BBar{G} = \begin{bmatrix}
>     0 & 1 & 1 & 0 & 1 \\
>     1 & 0 & 1 & 1 & 1 \\
> \end{bmatrix}
> $$

### Question 5.a.ii)
Obtain the syndrome table and decode the following received words.

$$
\bar{r}_0 = [10001], \bar{r}_1 = [10011], \bar{r}_2 = [11001]
$$

> **Answer** (class notes)
>
> The decoding process will be done by computing the syndrome of the received
> word and checking the syndrome table, so first we'll build the syndrome matrix
>
> In order to build the syndrome matrix, we need to compute the parity-check
> matrix $\overline{\overline{H}}$ (or its transpose), which is only feasible
> for us if the generating matrix is in the form
>
> $$
> \def\BBar#1{\overline{\overline{#1}}}
> \BBar{G} = \left[\begin{array}{c:c}
>         \BBar{I}_{k} & \BBar{P} \\
>     \end{array}\right] \text{ or } \begin{bmatrix}
>     \begin{array}{c:c}
>         \BBar{P} & \BBar{I}_{k} \\
>     \end{array}
> \end{bmatrix}
> $$
>
> If we look at our current $\overline{\overline{G}}$ matrix, it looks like
> this:
>
> $$
> \def\BBar#1{\overline{\overline{#1}}}
> \BBar{G} = \begin{bmatrix}
>     0 & 1 & 1 & 0 & 1 \\
>     1 & 0 & 1 & 1 & 1 \\
> \end{bmatrix}
> $$
>
> It currently doesn't look like the form we need, but by inspection we can see
> that swapping the rows will give us this form:
>
> $$
> \def\BBar#1{\overline{\overline{#1}}}
> \BBar{G} = \left[\begin{array}{cc:}
>     1 & 0 & 1 & 1 & 1 \\
>     0 & 1 & 1 & 0 & 1 \\
> \end{array}\right]
> $$
>
> Which has a $2×2$ identity matrix on the left. If we append a $3×3$ matrix
> under the right part of the matrix, we will obtain the transpose of the
> parity-check matrix, which we will use to compute the syndrome table.
>
> $$
> \def\BBar#1{\overline{\overline{#1}}}
> \BBar{H}^T = \begin{bmatrix}
>     1 & 1 & 1 \\
>     1 & 0 & 1 \\ \hdashline
>     1 & 0 & 0 \\
>     0 & 1 & 0 \\
>     0 & 0 & 1 \\
> \end{bmatrix}
> $$
>
> Let's begin our syndrome table
>
> | Error pattern $\bar{e}$ | Syndrome $\bar{s} = \bar{e} ⋅ \overline{\overline{H}}^T$ |
> | :---------------------: | :------------------------------------------------------: |
> |         `00000`         |                          `000`                           |
> |         `00001`         |                          `001`                           |
> |         `00010`         |                          `010`                           |
> |         `00100`         |                          `100`                           |
> |         `01000`         |                          `101`                           |
> |         `10000`         |                          `111`                           |
> |         `00011`         |                          `011`                           |
> |         `00110`         |                          `110`                           |
>
> > **Note** about building the syndrome table
> >
> > The best way to build the syndrome table is to start by adding all the
> > error patterns with 1 bit flipped on the left side of the table, and compute
> > their syndromes. Then, add the syndromes that are not covered yet, and find
> > combinations of error bits that produce them with the least number of bits
> > flipped.
>
> Now, we will start decoding the received words. First, we must compute their
> syndromes
>
> $$
> \def\BBar#1{\overline{\overline{#1}}}
> \def\Ht{\begin{bmatrix}
>     1 & 1 & 1 \\
>     1 & 0 & 1 \\
>     1 & 0 & 0 \\
>     0 & 1 & 0 \\
>     0 & 0 & 1 \\
> \end{bmatrix}}
>
> \begin{aligned}
>     \bar{r}_0 → \bar{s}_0 &= \bar{r}_0 ⋅ \BBar{H}^T = [10001] ⋅ \Ht \\
>         &= [1\; 1\; 0] \\[1em]
>     \bar{r}_1 → \bar{s}_1 &= \bar{r}_1 ⋅ \BBar{H}^T = [10011] ⋅ \Ht \\
>         &= [1\; 0\; 0] \\[1em]
>     \bar{r}_2 → \bar{s}_2 &= \bar{r}_2 ⋅ \BBar{H}^T = [11001] ⋅ \Ht \\
>         &= [0\; 1\; 1]
> \end{aligned}
> $$
>
> Then, find the error patterns associated to those syndromes
>
> $$
> \begin{aligned}
>     \hat{\bar{e}}_0 &= [00110] \\
>     \hat{\bar{e}}_1 &= [00100] \\
>     \hat{\bar{e}}_2 &= [00011] \\
> \end{aligned}
> $$
>
> With the error patterns, estimate the codewords
>
> $$
> \begin{aligned}
>     \hat{\bar{c}}_0 &= \bar{r}_0 ⊕ \hat{\bar{e}}_0 = [10001] ⊕ [00110]\\
>         &= [10111] \\
>     \hat{\bar{c}}_1 &= \bar{r}_1 ⊕ \hat{\bar{e}}_1 = [10011] ⊕ [00100]\\
>         &= [10111] \\
>     \hat{\bar{c}}_2 &= \bar{r}_2 ⊕ \hat{\bar{e}}_2 = [11001] ⊕ [00011]\\
>         &= [11010] \\
> \end{aligned}
> $$
>
> And finally, decode the codeword:
>
> $$
> \begin{aligned}
>     \hat{\bar{b}}_0 &= [0\; 1]\\
>     \hat{\bar{b}}_1 &= [0\; 1] \\
>     \hat{\bar{b}}_2 &= [1\; 1]\\
> \end{aligned}
> $$

## Exercise 5.b)
A convolutional code has the following generating vectors

$$
\bar{g}_1^1 = [1\; 1\; 1] \\
\bar{g}_2^1 = [1\; 0\; 0]
$$

The information data are transmitted with a 4-QAM modulation with the following
binary assignment.

| Symbol | $+1+j$ | $-1-j$ | $+1-j$ | $-1+j$ |
| :----: | :----: | :----: | :----: | :----: |
|  Bits  |   11   |   00   |   10   |   01   |

### Question 5.b.i) ✓
Get the schematic representation of the encoder, and the trellis diagram.

> **Answer** (class notes)
>
> We'll model it as a shift registser
>
> ```mermaid
> %%{init: {'forceLegacyMathML':'true'} }%%
> flowchart LR
> bi(["$$\bar{b}_i$$"])
> 
> subgraph sra [" "]
>     bi_["$$\bar{b}_i$$"]
>     bi_1["$$\bar{b}_{i-1}$$"]
>     bi_2["$$\bar{b}_{1-2}$$"]
>     bi_ -."shift".-> bi_1 -.-> bi_2
> end
> 
> bi --> bi_
> 
> xor1(("$$\oplus$$")) --> ci1(["$$\bar{c}_{i,1}$$"])
> xor2(("$$\oplus$$")) --> ci2(["$$\bar{c}_{i,2}$$"])
> 
> bi_ & bi_1 & bi_2 --> xor1
> bi_ ----> xor2
> 
> ci1 & ci2 --> ci(["$$\bar{c}_i$$"])
> ```

### Question 5.b.ii) ✓
Encode the information sequence $B^{(0)}[l] = [101100]$ under the assumption
that the starting state is the zero state, $ψ_0$. Plot the path of the output
sequence through the trellis diagram.

> **Answer** (class notes)
>
> First we'll see all the possible transitions:
>
> ```mermaid
> %%{init: {'forceLegacyMathML':'true'} }%%
> flowchart LR
> 
> subgraph s11 [" "]
>     s111(["[11]"]); s112((" "))
> end
> subgraph s10 [" "]
>     s101(["[10]"]); s102((" "))
> end
> subgraph s01 [" "]
>     s011(["[01]"]); s012((" "))
> end
> subgraph s00 [" "]
>     s001(["[00]"]); s002((" "))
> end
> 
> s001 --"0 | 00"--> s002
> s001 --"1 | 11"--> s102
> 
> s011 --"0 | 10"--> s002
> s011 --"1 | 01"--> s102
> 
> s101 --"0 | 10"--> s012
> s101 --"1 | 01"--> s112
> 
> s111 --"0 | 00"--> s012
> s111 --"1 | 11"--> s112
> ```
>
> Then we'll plot the sequence through the trellis diagram
>
> ```mermaid
> %%{init: {'forceLegacyMathML':'true'} }%%
> flowchart LR
> subgraph s11 [" "]
>     s110(["[11]"]) ~~~ s111((" ")) ~~~ s112((" ")) ~~~ s113((" ")) ~~~ s114((" ")) ~~~ s115((" ")) ~~~ s116((" "))
> end
> subgraph s10 [" "]
>     s100(["[10]"]) ~~~ s101((" ")) ~~~ s102((" ")) ~~~ s103((" ")) ~~~ s104((" ")) ~~~ s105((" ")) ~~~ s106((" "))
> end
> subgraph s01 [" "]
>     s010(["[01]"]) ~~~ s011((" ")) ~~~ s012((" ")) ~~~ s013((" ")) ~~~ s014((" ")) ~~~ s015((" ")) ~~~ s016((" "))
> end
> subgraph s00 [" "]
>     s000(["[00]"]) ~~~ s001((" ")) ~~~ s002((" ")) ~~~ s003((" ")) ~~~ s004((" ")) ~~~ s005((" ")) ~~~ s006((" "))
> end
> 
> s000 =="1 | 11"==> s101
> s101 =="0 | 10"==> s012
> s012 =="1 | 01"==> s103
> s103 =="1 | 01"==> s114
> s114 =="0 | 00"==> s015
> s015 =="0 | 10"==> s006
> ```

### Question 5.b.iii)
Get the code performance working both with hard and soft decoding.

> **Answer** (class notes)
>
> We must find the minimum distance of the code using another trellis diagram

### Question 5.b.iv) ✓
Decode the received sequence

$$
\bar{r} = [101001010011]
$$

assuming that $B^{(0)}[l] = 0$ for $l < 0$ and $l ≥ 4$ (i.e. the initial and
final states are $ψ_0$)

> **Answer** (class notes)
>
> ```mermaid
> %%{init: {'forceLegacyMathML':'true'} }%%
> flowchart LR
> subgraph s11 [" "]
>     s110(["[11]"]) ~~~ s111((" ")) ~~~ s112((" ")) ~~~ s113((" ")) ~~~ s114((" ")) ~~~ s115((" ")) ~~~ s116((" "))
> end
> subgraph s10 [" "]
>     s100(["[10]"]) ~~~ s101((" ")) ~~~ s102((" ")) ~~~ s103((" ")) ~~~ s104((" ")) ~~~ s105((" ")) ~~~ s106((" "))
> end
> subgraph s01 [" "]
>     s010(["[01]"]) ~~~ s011((" ")) ~~~ s012((" ")) ~~~ s013((" ")) ~~~ s014((" ")) ~~~ s015((" ")) ~~~ s016((" "))
> end
> subgraph s00 [" "]
>     s000(["[00]"]); s001((" ")) ~~~ s002((" ")) ~~~ s003((" ")) ~~~ s004((" ")) ~~~ s005((" ")) ~~~ s006((" "))
> end
> 
> s000 --"1"--> s001((1))
> s000 =="1"==> s101((1))
> 
> s001 --"1"--> s002((2))
> s001 --"1"--> s102((2))
> s101 =="0"==> s012((1))
> s101 --"2"--> s112((3))
> 
> s002 --"1"--> s003((3))
> s002 -."2".-> s103;
> s012 --"2"--> s003((3))
> s012 =="0"==> s103((1))
> s102 --"2"--> s013((4))
> s102 --"0"--> s113((2))
> s112 --"1"--> s013((4))
> s112 -."1".-> s113;
> 
> s003 --"1"--> s004((4))
> s003 --"1"--> s104((4))
> s013 -."2".-> s004;
> s013 --"0"--> s104((4))
> s103 --"2"--> s014((3))
> s103 =="0"==> s114((1))
> s113 --"1"--> s014((3))
> s113 -."1".-> s114;
> 
> s004 --"0"--> s005((4))
> s014 --"1"--> s005((4))
> s104 -."1".-> s015;
> s114 =="0"==> s015((1))
> 
> s005 -."2".-> s006;
> s015 =="1"==> s006((2))
> ```
>
> $$
> \{\hat{B}[n]\}_{n=0}^{5} = \{1\; 0\; 1\; 1\; 0\; 0\}
> $$
