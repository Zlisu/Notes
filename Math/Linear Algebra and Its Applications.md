<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [立体几何初步](#%E7%AB%8B%E4%BD%93%E5%87%A0%E4%BD%95%E5%88%9D%E6%AD%A5)
	- [一、平面的基本性质与推论](#%E4%B8%80%E5%B9%B3%E9%9D%A2%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%80%A7%E8%B4%A8%E4%B8%8E%E6%8E%A8%E8%AE%BA)
		- [1、平面的基本性质：](#1%E5%B9%B3%E9%9D%A2%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%80%A7%E8%B4%A8)
		- [2、空间点、直线、平面之间的位置关系：](#2%E7%A9%BA%E9%97%B4%E7%82%B9%E7%9B%B4%E7%BA%BF%E5%B9%B3%E9%9D%A2%E4%B9%8B%E9%97%B4%E7%9A%84%E4%BD%8D%E7%BD%AE%E5%85%B3%E7%B3%BB)
		- [3、异面直线：](#3%E5%BC%82%E9%9D%A2%E7%9B%B4%E7%BA%BF)
	- [二、空间中的平行关系](#%E4%BA%8C%E7%A9%BA%E9%97%B4%E4%B8%AD%E7%9A%84%E5%B9%B3%E8%A1%8C%E5%85%B3%E7%B3%BB)
		- [1、直线与平面平行（核心）](#1%E7%9B%B4%E7%BA%BF%E4%B8%8E%E5%B9%B3%E9%9D%A2%E5%B9%B3%E8%A1%8C%E6%A0%B8%E5%BF%83)
		- [2、平面与平面平行](#2%E5%B9%B3%E9%9D%A2%E4%B8%8E%E5%B9%B3%E9%9D%A2%E5%B9%B3%E8%A1%8C)
		- [3、常利用三角形中位线、平行四边形对边、已知直线作一平面找其交线](#3%E5%B8%B8%E5%88%A9%E7%94%A8%E4%B8%89%E8%A7%92%E5%BD%A2%E4%B8%AD%E4%BD%8D%E7%BA%BF%E5%B9%B3%E8%A1%8C%E5%9B%9B%E8%BE%B9%E5%BD%A2%E5%AF%B9%E8%BE%B9%E5%B7%B2%E7%9F%A5%E7%9B%B4%E7%BA%BF%E4%BD%9C%E4%B8%80%E5%B9%B3%E9%9D%A2%E6%89%BE%E5%85%B6%E4%BA%A4%E7%BA%BF)
	- [三、空间中的垂直关系](#%E4%B8%89%E7%A9%BA%E9%97%B4%E4%B8%AD%E7%9A%84%E5%9E%82%E7%9B%B4%E5%85%B3%E7%B3%BB)
		- [1、直线与平面垂直](#1%E7%9B%B4%E7%BA%BF%E4%B8%8E%E5%B9%B3%E9%9D%A2%E5%9E%82%E7%9B%B4)
		- [2、平面与平面垂直](#2%E5%B9%B3%E9%9D%A2%E4%B8%8E%E5%B9%B3%E9%9D%A2%E5%9E%82%E7%9B%B4)
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
	- [Span\{**v**~1~, $\cdot\cdot\cdot$, **v**~p~}](#spanv1-cdotcdotcdot-vp)
		- [Geometric Description](#geometric-description)
- [1.4 The Matrix Equation Ax = b](#14-the-matrix-equation-ax--b)
	- [Definition](#definition)
		- [Theorem 3](#theorem-3)
	- [Existence of Solutions](#existence-of-solutions)
		- [Theorem 4](#theorem-4)
	- [Computation of Matrix–Vector Product $A\bold{x}$](#computation-of-matrix%E2%80%93vector-product-aboldx)
		- [Theorem 5](#theorem-5)
- [1.5 Solution sets of linear systems](#15-solution-sets-of-linear-systems)
	- [Homogeneous Linear Systems](#homogeneous-linear-systems)
	- [Parametric Vector Form](#parametric-vector-form)
	- [Solutions of Nonhomogeneous Systems](#solutions-of-nonhomogeneous-systems)

<!-- /code_chunk_output -->






## 立体几何初步

### 一、平面的基本性质与推论
#### 1、平面的基本性质：

* 公理1 如果一条直线的两点在一个平面内，那么这条直线在这个平面内；
* 公理2 过不在一条直线上的三点，有且只有一个平面；
* 公理3 如果两个不重合的平面有一个公共点，那么它们有且只有一条过该点的公共直线。

#### 2、空间点、直线、平面之间的位置关系：

* 直线与直线-平行、相交、异面；
* 直线与平面-平行、相交、直线属于该平面（线在面内，最易忽视）；
* 平面与平面-平行、相交。
  
#### 3、异面直线：

* 平面外一点A与平面一点B的连线和平面内不经过点B的直线是异面直线（判定）；
* 所成的角范围(0，90] 度（平移法，作平行线相交得到夹角或其补角）；
* 两条直线不是异面直线，则两条直线平行或相交（反证）；
* 异面直线不同在任何一个平面内。
* 求异面直线所成的角：平移法，把异面问题转化为相交直线的夹角

### 二、空间中的平行关系

#### 1、直线与平面平行（核心）

* 定义：直线和平面没有公共点
* 判定：不在一个平面内的一条直线和平面内的一条直线平行，则该直线平行于此平面（由线线平行得出）
* 性质：一条直线和一个平面平行，经过这条直线的平面和这个平面相交，则这条直线就和两平面的交线平行

#### 2、平面与平面平行

* 定义：两个平面没有公共点
* 判定：一个平面内有两条相交直线平行于另一个平面，则这两个平面平行
* 性质：两个平面平行，则其中一个平面内的直线平行于另一个平面；如果两个平行平面同时与第三个平面相交，那么它们的交线平行。

#### 3、常利用三角形中位线、平行四边形对边、已知直线作一平面找其交线

### 三、空间中的垂直关系

#### 1、直线与平面垂直

* 定义：直线与平面内任意一条直线都垂直
* 判定：如果一条直线与一个平面内的两条相交的直线都垂直，则该直线与此平面垂直
* 性质：垂直于同一直线的两平面平行
* 推论：如果在两条平行直线中，有一条垂直于一个平面，那么另一条也垂直于这个平面
* 直线和平面所成的角：[0，90] 度，平面内的一条斜线和它在平面内的射影说成的锐角，特别规定垂直90度，在平面内或者平行0度
  
#### 2、平面与平面垂直

* 定义：两个平面所成的二面角（从一条直线出发的两个半平面所组成的图形）是直* 二面角（二面角的平面角：以二面角的棱上任一点为端点，在两个半平面内分别作垂直于棱的两条射线所成的角）
* 判定：一个平面过另一个平面的垂线，则这两个平面垂直
* 性质：两个平面垂直，则一个平面内垂直于交线的直线与另一个平面垂直

---

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

