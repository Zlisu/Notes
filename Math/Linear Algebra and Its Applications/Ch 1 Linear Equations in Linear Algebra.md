<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [Chapter 1 Linear Equations in Linear Algebra](#chapter-1-linear-equations-in-linear-algebra)
  - [1.2 Row reduction and echelon forms](#12-row-reduction-and-echelon-forms)
    - [Echelon matrix](#echelon-matrix)
    - [Theorem 1](#theorem-1)
    - [Pivot positions](#pivot-positions)
    - [Existence and Uniqueness Questions (Theorem 2)](#existence-and-uniqueness-questions-theorem-2)
  - [1.3 Vector Equations](#13-vector-equations)
    - [Denotation](#denotation)
    - [Operation](#operation)
      - [sum](#sum)
      - [scalar multiple](#scalar-multiple)
      - [Parallelogram Rule for Addition](#parallelogram-rule-for-addition)
    - [Linear Combinations](#linear-combinations)
    - [Span\{**v**~1~, $\cdot\cdot\cdot$, **v**~p~}](#spanv1-mathsemanticsmrowmo%e2%8b%85momo%e2%8b%85momo%e2%8b%85momrowannotation-encoding%22applicationx-tex%22cdotcdotcdotannotationsemanticsmath%e2%8b%85%e2%8b%85%e2%8b%85-vp)
      - [Geometric Description](#geometric-description)
  - [1.4 The Matrix Equation Ax = b](#14-the-matrix-equation-ax--b)
    - [Definition](#definition)
      - [Theorem 3](#theorem-3)
    - [Existence of Solutions](#existence-of-solutions)
      - [Theorem 4](#theorem-4)
    - [Computation of Matrix–Vector Product $A\bold{x}$](#computation-of-matrix%e2%80%93vector-product-mathsemanticsmrowmiamimi-mathvariant%22bold%22xmimrowannotation-encoding%22applicationx-tex%22aboldxannotationsemanticsmathax)
      - [Theorem 5](#theorem-5)
  - [1.5 Solution sets of linear systems](#15-solution-sets-of-linear-systems)
    - [Homogeneous Linear Systems](#homogeneous-linear-systems)
      - [Geometric](#geometric)
    - [Parametric Vector Form](#parametric-vector-form)
    - [Solutions of Nonhomogeneous Systems](#solutions-of-nonhomogeneous-systems)
      - [parametric vector form](#parametric-vector-form-1)
      - [translation](#translation)
      - [Theorem 6](#theorem-6)
  - [1.7 Linear Independence](#17-linear-independence)
    - [Definition](#definition-1)
    - [Sets of Two or More Vectors](#sets-of-two-or-more-vectors)
      - [Theorem 7](#theorem-7)
      - [Theorem 8](#theorem-8)
      - [Theorem 9](#theorem-9)
  - [1.8 Introduction to Linear Transformations](#18-introduction-to-linear-transformations)
    - [Definition](#definition-2)
  - [1.9 The Matrix of A Linear Transformation](#19-the-matrix-of-a-linear-transformation)
    - [Theorem 10](#theorem-10)
    - [Onto](#onto)
    - [one-to-one](#one-to-one)
      - [Thorem 11](#thorem-11)
      - [Thorem 12](#thorem-12)
- [Chapter 2 Matrix Algebra](#chapter-2-matrix-algebra)
  - [2.1 Matrix Operations](#21-matrix-operations)
    - [Theorem 1](#theorem-1-1)
    - [Theorem 2](#theorem-2)

<!-- /code_chunk_output -->


---
# Chapter 1 Linear Equations in Linear Algebra

## 1.2 Row reduction and echelon forms

A **nonzero row** or column in a matrix means a row or column that contains at least one nonzero entry; 

A **leading entry** of a row refers to the leftmost nonzero entry (in a nonzero row).

### Echelon matrix 

Row echelon form:
1. All nonzero rows are above any rows of all zeros
2. Each leading entry of a row is in a column to the right of the leading entry of the row above it.
3. All entries in a column below a leading entry are zeros.

$$
\begin{bmatrix}
0 & \blacksquare & * & * & * & * & * & * & * & * \\
0 & 0 & 0 & \blacksquare & * & * & * & * & * & * \\
0 & 0 & 0 & 0 & \blacksquare & * & * & * & * & * \\
0 & 0 & 0 & 0 & 0 & \blacksquare & * & * & * & * \\
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & \blacksquare & * \\ 
\end{bmatrix}
$$

**Reduced echelon matrix**:
The leading entries are 1’s, and there are 0’s below and above each leading 1.

$$
\begin{bmatrix}
0 & 1 & * & 0 & 0 & 0 & * & * & 0 & * \\
0 & 0 & 0 & 1 & 0 & 0 & * & * & 0 & * \\
0 & 0 & 0 & 0 & 1 & 0 & * & * & 0 & * \\
0 & 0 & 0 & 0 & 0 & 1 & * & * & 0 & * \\
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & 1 & *
\end{bmatrix}
$$


Any nonzero matrix may be row reduced (that is, transformed by elementary row operations) into more than one matrix in echelon form. However, the reduced echelon form one obtains from a matrix is unique.

### Theorem 1

> Each matrix is row equivalent to one and only one reduced echelon matrix.

If a matrix A is row equivalent to an echelon matrix U, we call U an echelon form (or row echelon form) of A; if U is in reduced echelon form, we call U the reduced echelon form of A.

### Pivot positions
A pivot position in a matrix A is a location in A that corresponds to a leading 1 in the reduced echelon form of A. 

When row operations on a matrix produce an echelon form, further row operations to obtain the reduced echelon form do not change the positions of the leading entries. Since the reduced echelon form is unique, the leading entries are always in the same positions in any echelon form obtained from a given matrix. These leading entries correspond to leading 1’s in the reduced echelon form.
一个矩阵在row echelon form 时，the leading entry 的位置就是这个矩阵在进一步 reduced 之后所得到的 leading 1的位置。所以 the leading entry 的位置 及其 reduced echelon matrix 中 leading 1 的位置，即为 pivot positions.

**Pivot columns**
A pivot column is a column of A that contains a pivot position.

### Existence and Uniqueness Questions (Theorem 2)
The variables corresponding to pivot columns in the matrix are called **basic variables**.
The other variables are called **free variables**.

**Existence**:
如果一个 system 在转化成 echelon form 之后没有得到 [0 0 0 0 2] 这样的 row， 那么这个 system 就是 **consistent** 的。

**Uniqueness**:
如果没有 free variable，这个 system 有**唯一解**。
如果有 free variable 存在，这个system 有**无数个解**。

---

## 1.3 Vector Equations

A matrix with only one column is called a **column vector**, or simply a **vector**.
Example: $\begin{bmatrix}3\\-1\end{bmatrix}$, $\begin{bmatrix}w_1 \\
w_2\end{bmatrix}$
w~1~ and w~2~ are **real numbers**.

### Denotation

$\reals ^n$: $\reals$ 代表实数； ^n^ 代表 vector 中元素的个数。
$\begin{bmatrix}3\\-1\end{bmatrix}$ 可以记作(3, -1)。但[3, -1] 代表的是 $1*2$ 的 matrix。

### Operation

#### sum

$$
\begin{bmatrix}
1 \\
-2
\end{bmatrix}
+ 
\begin{bmatrix}
2 \\
5
\end{bmatrix}
{=}
\begin{bmatrix}
1 + 2 \\
-2 + 5
\end{bmatrix}
{=}
\begin{bmatrix}
3 \\
3
\end{bmatrix}
$$

#### scalar multiple

Given a vector **u** and a real number c, if $\bold{u}=\begin{bmatrix}3 \\ -1 \end{bmatrix}$ and c = 5, then $c\bold{u}=5\begin{bmatrix}3\\-1\end{bmatrix} {=} \begin{bmatrix}15\\-5\end{bmatrix}$. 

It's called the scalar multiple of **u**. The number c is called a scalar.


#### Parallelogram Rule for Addition

If **u** and **v** in $\reals ^2$ are represented as points in the plane, then **u** + **v** corresponds to the fourth vertex of the parallelogram whose other vertices are **u**, **0**, and **v**.

![enter image description here](https://github.com/Zlisu/Notes/blob/master/Images/parallelogram_rule.png?raw=True)

### Linear Combinations

Given vectors **v**~1~, **v**~2~, $\cdot\cdot\cdot$, **v**~p~ and given scalars c~1~, c~2~ $\cdot\cdot\cdot$ c~p~, the vector **y** defined by
**y** = c~1~**v**~1~ + c~2~**v**~2~ + $\cdot\cdot\cdot$ + c~p~**v**~p~
is called a linear combination of **v**~1~, **v**~2~, $\cdot\cdot\cdot$, **v**~p~ with **weights** c~1~, c~2~ $\cdot\cdot\cdot$ c~p~.

### Span\{**v**~1~, $\cdot\cdot\cdot$, **v**~p~}

Asking whether a vector **b** is in Span\{**v**~1~, $\cdot\cdot\cdot$, **v**~p~} amounts to asking whether the vector equation
x~1~**v**~1~ + x~2~**v**~2~ + $\cdot\cdot\cdot$ + x~p~**v**~p~ = **b**
has a solution, or, equivalently, asking whether the linear system with augmented matrix [**v**~1~ **v**~2~ $\cdot\cdot\cdot$ **v**~p~$\enspace$**b**] has a solution.

#### Geometric Description
Let **v** be a nonzero $\reals ^3$. Then Span{**v**} is the set of all scalar multiples of v, which is the set of points on the line in $\reals ^3$ through **v** and **0**. See Figure 10.

If **u** and **v** are nonzero vectors in $\reals ^3$, with **v** not a multiple of **u**, then Span{**u**, **v**} is the plane in $\reals ^3$ that contains **u**, **v**, and **0**. In particular, Span{**u**, **v**} contains the line in $\reals ^3$ through **u** and **0** and the line through **v** and **0**.

![as a line through the origin](https://github.com/Zlisu/Notes/blob/master/Images/span_v.png?raw=True) ![as a plain through the origin](https://github.com/Zlisu/Notes/blob/master/Images/span_u_v.png?raw=True)

---

## 1.4 The Matrix Equation Ax = b

### Definition

If A is an $m \times n$ matrix, with columns **a**~1~, $\cdot\cdot\cdot$, **a**~n~, and if **x** is in $\reals ^n$, then the product of A and **x**, denoted by A**x**, is the linear combination of the columns of A using the corresponding entries in **x** as weights:
$$ A\bold{x} = \begin{bmatrix} \bold{a}_1 & \bold{a}_2 & \cdot\cdot\cdot & \bold{a}_n \end{bmatrix} \begin{bmatrix}x_1 \\ \cdot \\ \cdot \\ \cdot \\ x_n \end{bmatrix} = x_1\bold{a}_1 + x_1\bold{a}_2 + \cdot\cdot\cdot + x_n\bold{a}_n$$ 

*Note that A**x** is defined only if the number of columns of A equals the number of entries
in **x**.*

For example, 
$x_1\begin{bmatrix}1\\0\end{bmatrix} + x_2\begin{bmatrix}2\\-5\end{bmatrix} + x_3\begin{bmatrix}-1\\3\end{bmatrix} = \begin{bmatrix}4\\1\end{bmatrix}$ is called a **vector equation**;
while $\begin{bmatrix}1 & 2 & -1\\0 & -5 & 3\end{bmatrix} \begin{bmatrix}x_1 \\ x_2 \\ x_3\end{bmatrix} = \begin{bmatrix}4 \\ 1\end{bmatrix}$ is called a **matrix equation**.

#### Theorem 3

> If A is an $m \times n$ matrix, with columns **a**~1~, $\cdot\cdot\cdot$, **a**~n~, and if **b** is in $\reals ^m$, the matrix equation
> $$A\bold{x} = \bold{b}$$ has the same solution set as the vector equation
$$x_1\bold{a}_1 + x_1\bold{a}_2 + \cdot\cdot\cdot + x_n\bold{a}_n = \bold{b}$$ which, in turn, has the same solution set as the system of linear equations whose augmented matrix is 
> $$\begin{bmatrix}\bold{a}_1 & \bold{a}_2 & \cdot\cdot\cdot & \bold{a}_n & \bold{b}\end{bmatrix}$$

Theorem 3 provides a powerful tool for gaining insight into problems in linear algebra, because a system of linear equations may now be viewed in three different but equivalent ways: 
1. as a matrix equation, 
2. as a vector equation, 
3. or as a system of linear equations.

### Existence of Solutions

The equation $A\bold{x} = \bold{b}$ has a solution if and only if $\bold{b}$ is a linear combination of the columns of $A$.

#### Theorem 4
> Let $A$ be an $m \times n$ matrix. Then the following statements are logically equivalent. That is, for a particular $A$, either they are all true statements or they are all false.
> a. For each $\bold{b}$ in $\reals ^m$, the equation $A\bold{x} = \bold{b}$ has a solution.
> b. Each $\bold{b}$ in $\reals ^m$ is a linear combination of the columns of $A$.
> c. The columns of $A$ span $\reals ^m$.
> d. $A$ has a pivot position in every row.


Note:
the sentence “The columns of $A$ span $\reals ^m$" means that every $\bold{b}$ in $\reals ^m$ is a linear combination of the columns of A.

In general, a set of vectors $\{\bold{v}_1, ..., \bold{v}_p\}$ in $\reals ^m$ spans or generates $\reals ^m$ if every vector in $\reals ^m$ is a linear combination of  $\bold{v}_1, ..., \bold{v}_p$ - that is, if $Span\{\bold{v}_1, ..., \bold{v}_p\} = \reals ^m$.

### Computation of Matrix–Vector Product $A\bold{x}$
If the product $A\bold{x}$ is defined, then the $i$ th entry in $A\bold{x}$ is the sum of the products of corresponding entries from row $i$ of $A$ and from the vector $\bold{x}$.

$A$ 是一个 $m \times n$ 的 matrix, $\bold{x}$ 是 $\reals ^n$, 注意 $A$ 的列数必须与 $\bold{x}$ 的元素个数相等（都是 $n$）。它们相乘的结果是一个 vector, 这个 vector 的元素个数与 $A$ 的行数相等（都是 $m$）。

The matrix with 1’s on the diagonal and 0’s elsewhere is called an **identity matrix** and is denoted by $I$.
There is an analogous $n \times n$ identity matrix written as $I_n$. $I_n\bold{x} = \bold{x}$.

#### Theorem 5
> If $A$ is an $m \times n$ matris, $\bold{u}$ and $\bold{v}$ are vectors in $\reals ^n$, and $c$ is a scalar, then:
> a. $A(\bold{u} + \bold{v}) = A\bold{u} + A\bold{v}$
> b. $A(c\bold{u}) = c(A\bold{u})$

---

## 1.5 Solution sets of linear systems

### Homogeneous Linear Systems

A system of linear equations is said to be **homogeneous** if it can be written in the form $A\bold{x} = \bold{0}$, where $A$ is an $m \times n$ matrix and $\bold{0}$ is the zero vector in $\reals ^m$.
Such a system $A\bold{x} = \bold{0}$ always has at least one solution, namely, $\bold{x} = \bold{0}$ ($\bold{0}$ is the zero vector in $\reals ^n$). This zero solution is usually called the **trivial solution**. 
For a given equation $A\bold{x} = \bold{0}$, the important question is whether there exists a nontrivial solution, that is, a nonzero vector $\bold{x}$ that satisfies $A\bold{x} = \bold{0}$. According to Theorem 2,
> The homogeneous equation $A\bold{x} = \bold{0}$ has a nontrivial solution if and only if the equation has at least one free variable.

#### Geometric

If the equation $A\bold{x} = \bold{0}$ has only one free variable, the solution set is a line through the origin, as in Figure 1.

A plane through the origin, as in Figure 2, provides a good mental image for the solution set of $A\bold{x} = \bold{0}$ when there are two or more free variables.
![a line through the origin](https://github.com/Zlisu/Notes/blob/master/Images/one_free_variable.png?raw=True) ![a plain through the origin](https://github.com/Zlisu/Notes/blob/master/Images/two_free_variables.png?raw=True)

### Parametric Vector Form

$10x_1 - 3x_2 - 2x_3 = 0$ is an **implicit** despription of the plane.
The solution of this single linear equation is:
$$\bold{x} = \begin{bmatrix}x_1 \\ x_2 \\ x3\end{bmatrix} = x_2 \begin{bmatrix} .3 \\ 1 \\ 0\end{bmatrix} + x_3\begin{bmatrix} .2 \\ 0 \\ 1\end{bmatrix}  (with\enspace x_2, \, x_3 \, free)$$

This is an **explicit** description of the *plane* as the set spanned by u and v.

The equation above is called the parametric vector equation of the plane:
$$\bold{x} = s\bold{u} + t\bold{v}  (s, \, t\enspace   in \enspace \reals )$$
the parameters ($s$ and $t$) vary over all real numbers.

$\bold{x} = t\bold{v}$ (with $t$ in $\reals$) is a parametric vector equation of a *line*.(see Figure 1 above)

Whenever a solution set is described explicitly with vectors, we say that the solution is in **parametric vector form.**

### Solutions of Nonhomogeneous Systems

#### parametric vector form

The parametric vector equation of the solution set of $\bold{Ax} = \bold{b}$:
$$\bold{x} = \bold{p} + t\bold{v} \medspace \text{(3)}$$
The parametric vector equation of the solution set of $\bold{Ax} = \bold{0}$:
$$\bold{x} = t\bold{v} \medspace \text{(4)}$$

#### translation

Given $\bold{v}$ and $\bold{p}$ in $\reals ^2$ or $\reals ^3$, the effect of adding $\bold{p}$ to $\bold{v}$ is to move $\bold{v}$ in the direction parallel to the line through $\bold{p}$ and $\bold{0}$. We say that $\bold{v}$ is translated by $\bold{p}$ to $\bold{v} + \bold{p}$. See figure 3:
![adding](https://github.com/Zlisu/Notes/blob/master/Images/adding_p_v.png?raw=True)

If each point on a line $L$ in $\reals ^2$ or $\reals ^3$ is translated by a vector $\bold{p}$, the result is a line parallel to $L$. See figure 4:
![adding](https://github.com/Zlisu/Notes/blob/master/Images/translated_line.png?raw=True)

Suppose $L$ is the line through $\bold{0}$ and $\bold{v}$, described by equation (4). Adding $\bold{p}$ to each point on $L$ produces the translated line described by equation (3). Note that $\bold{p}$ is on the line in equation (3). We call (3) the equation of the line through p parallel to v. The the solution set of $\bold{Ax} = \bold{b}$ is a line through $\bold{p}$ parallel to the solution set of $\bold{Ax} = \bold{0}$. See figure 5:
![adding](https://github.com/Zlisu/Notes/blob/master/Images/parallel_solution_sets_1free.png?raw=True)

Figure 6 illustrates the case in which there are two free variables. Even
when n > 3, our mental image of the solution set of a consistent system $\bold{A} = \bold{b}$ (with $\bold{b}{=}\mathllap{/\,}\bold{0}$) is either a single nonzero point or a line or plane not passing through the origin.
![adding](https://github.com/Zlisu/Notes/blob/master/Images/parallel_solution_sets_2free.png?raw=True)

#### Theorem 6

> Suppose the equation $A\bold{x} = \bold{b}$ is consistent for some given $\bold{b}$, and let $\bold{p}$ be a solution. Then the solution set of $A\bold{x} = \bold{b}$ is the set of all vectors of the form $\bold{w} = \bold{p} + \bold{v_h}$, where $\bold{v_h}$ is any solution of the homogeneous equation $A\bold{x} = \bold{0}$



Theorem 6 says that if $A\bold{x} = \bold{b}$ has a solution, then the solution set is obtained by translating the solution set of $A\bold{x} = \bold{0}$, using any particular solution $\bold{p}$ of $A\bold{x} = \bold{b}$ for the translation.

---

## 1.7 Linear Independence

### Definition

> An indexed set of vectors $\{\bold{v}_1, ..., \bold{v}_p\}$ in $\reals ^n$ is said to be linearly independent if the vectors equation $$x_1\bold v_1 + x_2\bold v_2 + ... + x_p\bold v_p = \bold0 $$ has only the trivial solution. 
> 
> The set $\{\bold v_1, ..., \bold v_p\}$ is said to be linearly dependent if there exist weights $c_1, ..., c_p$, not all zero, such that $$c_1\bold v_1 + c_2\bold v_2 + ... + c_p\bold v_p = \bold 0 $$

### Sets of Two or More Vectors

#### Theorem 7

> An indexed set $S = \{\bold v_1, ..., \bold v_p\}$ of two or more vectors is linearly dependent if and only if at least one of the vectors in $S$ is a linear combination of the others. In fact if $S$ is linearly dependent and $\bold v_1 \neq\bold 0$, then some $\bold v_j$ (with $j > 1$) is a linear combination of the preceding vectors, $\bold v_1, ..., \bold v_{j-1}$.

#### Theorem 8

> If a set contains more vectors than there are entries in each vector, then the set is linearly dependent. That is, any set $\{\bold v_1, ..., \bold v_p\}$ in $\reals ^n$ is linearly dependent if $p > n$.

#### Theorem 9

> If a set $S = \{\bold v_1, ..., \bold v_p\}$ in $\reals ^n$ contains the zero vector, then the set is linearly dependent.

---

## 1.8 Introduction to Linear Transformations

### Definition

> A transformation (or mapping) $T$ is **linear** if:
> (i) $T(\bold u + \bold b) = T(\bold u) + T(\bold v)$
> (ii) $T(c\bold u) = cT(\bold u)$

Every **matrix transformation** is a **linear transformation**.

## 1.9 The Matrix of A Linear Transformation

### Theorem 10

> Let $T: \reals ^n \rarr \reals ^m$ be a linear transformation. Then there exists a unique matrix $A$ such that
> $T(\bold x) = A\bold x $ for all $\bold x$ in $\reals ^n$
> In fact, $A$ is the $m * n$ matrix whose *j*th column is the vector $T(\bold e_j)$, where $\bold e_j$ is the $j$th column of the identity matrix in $\reals ^n$: $$A = [T(\bold e_1) \quad ... \quad T(\bold e_n)]$$

$A = [T(\bold e_1) \quad ... \quad T(\bold e_n)]$ is called the **standard matrix for the linear transformation** $T$.

### Onto

> A mapping $T: \reals ^n \rarr \reals ^m$ is said to be **onto** $\reals ^m$ if each **b** in $\reals ^m$ is the image of at least *one* **x** in $\reals ^n$.

### one-to-one

> A mapping $T: \reals ^n \rarr \reals ^m$ is said to be **one-to-one** if each **b** in $\reals ^m$ is the image of *at most one* **x** in $\reals ^n$.

#### Thorem 11

> Let $T: \reals ^n \rarr \reals ^m$ be a linear transformation. Then $T$ is one-to-one if and only if the equation $T(\bold x) = \bold 0$ has only the trivial solution.

(page 77)

#### Thorem 12

> Let $T: \reals ^n \rarr \reals ^m$ be a linear transformation, and let $A$ be the standard matrix for $T$. Then:
> 
> a. $T$ maps $\reals ^n to \reals ^m$ if and only if the columns of $A$ span $\reals ^m$;
> b. $T$ is one-to-one if and only if the columns of $A$ are linearly independent.

(page 78)

---

# Chapter 2 Matrix Algebra

## 2.1 Matrix Operations

### Theorem 1

>Let $A$, $B$, and $C$ be matrices of the same size, and let $r$ and $s$ be scalars.
>
>a. $A + B = B + A$
b. $(A + B) + C = A + (B + C)$
c. $A + 0 = A$
d. $r(A + B) = rA + rB$
e. $(r + s)A = rA + sA$
f. $r(sA) = (rs)A$

### Theorem 2

>Let $A$ be an $m \times n$ matrix, and let $B$ and $C$ have sizes for which the indicated sums and products are defined.
>
>a. $A(BC) = (AB)C$   
b. $A(B + C) = AB + AC$
c. $(B + C)A = BA + CA$
d. $r(AB) = (rA)B = A(rB)$
e. $I_mA = A = AI_n$

