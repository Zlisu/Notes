
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