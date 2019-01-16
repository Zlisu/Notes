
<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->


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

***Each matrix is row equivalent to one and only one reduced echelon matrix.***

If a matrix A is row equivalent to an echelon matrix U, we call U an echelon form (or row echelon form) of A; if U is in reduced echelon form, we call U the reduced echelon form of A.

### Pivot positions
A pivot position in a matrix A is a location in A that corresponds to a leading 1 in the reduced echelon form of A. 

When row operations on a matrix produce an echelon form, further row operations to obtain the reduced echelon form do not change the positions of the leading entries. Since the reduced echelon form is unique, the leading entries are always in the same positions in any echelon form obtained from a given matrix. These leading entries correspond to leading 1’s in the reduced echelon form.
一个矩阵在row echelon form 时，the leading entry 的位置就是这个矩阵在进一步 reduced 之后所得到的 leading 1的位置。所以 the leading entry 的位置 及其 reduced echelon matrix 中 leading 1 的位置，即为 pivot positions.

**Pivot columns**
A pivot column is a column of A that contains a pivot position.

### Existence and Uniqueness Questions
The variables corresponding to pivot columns in the matrix are called **basic variables**.
The other variables are called **free variables**.

**Existence**:
如果一个 system 在转化成 echelon form 之后没有得到$$[0 0 0 0 2] 这样的 row， 那么这个 system 就是 **consistent** 的。

**Uniqueness**:
如果没有 free variable，这个 system 有**唯一解**。
如果有 free variable 存在，这个system 有**无数个解**。

## 1.3 Vector

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

#### Linear Combinations

Given vectors **v**~1~, **v**~2~, ..., **v**~p~ and given scalars c~1~, c~2~ ... c~p~, the vector **y** defined by
**y** = c~1~**v**~1~ + c~2~**v**~2~ + ... + c~p~**v**~p~
is called a linear combination of **v**~1~, **v**~2~, ..., **v**~p~ with **weights** c~1~, c~2~ ... c~p~.

#### Span\{**v**~1~, ..., **v**~p~}

Asking whether a vector **b** is in Span\{**v**~1~, ..., **v**~p~} amounts to asking whether the vector equation
x~1~**v**~1~ + x~2~**v**~2~ + ... + x~p~**v**~p~ = **b**
has a solution, or, equivalently, asking whether the linear system with augmented matrix [**v**~1~ **v**~2~ ... **v**~p~    **b**] has a solution.
