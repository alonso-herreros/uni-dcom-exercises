## Digital Communications <!-- omit in toc -->

# Chapter 6 Exercises

*Academic year 2024-2025*  

$$
\global\def\Bar{\overline}
\global\def\BBar#1{\overline{\overline{#1}}}
$$

---

### Table of Contents

* [Exercise 1 ✓](#exercise-1-)

---

## Exercise 1 ✓

The encoding matrix for a linear block code $(4, 8)$ is given next. Compute the coding rate,
the minimum distance and the syndrome table.

$$
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
> possible error patterns by $\BBar{H}$, which is only easy to compute if we
> have a generating matrix of the form
>
> $$
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
> If we add an identity to the bottom of the right part of our $\BBar{G}'$
> (which is the parity matrix $\BBar{P}$), we can directly obtain the transpose
> of the parity-check matrix, which we will use to compute the syndrome table.
>
> $$
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
> by $\BBar{H}^T$. First, we'll add all the error patterns with 1 bit flipped.
> After that, we'll first add all the syndromes that are left, and find the
> error patterns that produce them with the least number of bits flipped.
>
> | Error pattern $\bar{e}$ | Syndrome $\bar{s} = \bar{e} ⋅ \BBar{H}^T$ |
> | :---------------------: | :---------------------------------------: |
> |       `00000000`        |                  `0000`                   |
> |       `00000001`        |                  `0001`                   |
> |       `00000010`        |                  `0010`                   |
> |       `00000100`        |                  `0100`                   |
> |       `00001000`        |                  `1000`                   |
> |       `00010000`        |                  `0111`                   |
> |       `00100000`        |                  `1110`                   |
> |       `01000000`        |                  `1011`                   |
> |       `10000000`        |                  `1101`                   |
> |       `00000011`        |                  `0011`                   |
> |       `00000101`        |                  `0101`                   |
> |       `00000110`        |                  `0110`                   |
> |       `00001001`        |                  `1001`                   |
> |       `00001010`        |                  `1010`                   |
> |       `00001100`        |                  `1100`                   |
> |       `00100001`        |                  `1111`                   |
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
> > 2. Much easier to do is finding the syndrome $\bar{s} and checking the
> > syndrome table, then flipping the corresponding bits.
> >
> >     $$
> >     \bar{s} = \bar{r} ⋅ \BBar{H}^T = 0100 \\
> >     \hat{\bar{c}} = \bar{r} + \bar{e} = 00010111
> >     $$
