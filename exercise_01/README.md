# Exercise 01
_Geometry Processing Research in Python_

## NumPy for geometry processing

In this tutorial (and in much of my own geometry processing research), geometric
data is represented on the computer as vectors and matrices, and manipulations
of geometric data are expressed using the language of linear algebra.

Gpytoolbox uses NumPy as its basic linear algebra library.
If you are familiar with MATLAB, then you will find that NumPy and MATLAB are
very similar - the creators of NumPy
[provide this simple cheat sheet](https://numpy.org/doc/stable/user/numpy-for-matlab-users.html) to compare the two languages.

I will not go into too much detail introducing NumPy, but in this exercise we
will quickly recall how to do a few very basic linear algebra tasks in NumPy.

### Defining vectors and matrices

The basic data type in numpy is an array with `k` axes.
If `k==1`, then we have a vector.
```python
import numpy as np
u = np.array([1., 2.])
print(u)
```
This prints:
```
[1. 2.]
```

If `k==2`, we have a matrix, which we specify in _row major_ order (i.e., the
matrix is an array of rows),
```python
import numpy as np
A = np.array([[1., 2.], [3., 4.], [5., 6.]])
print(A)
```
This prints:
```
[[1. 2.]
 [3. 4.]
 [5. 6.]]
```

### Elementwise arithmetic

Using the arithmetic operators `+`, `-`, `*`, `/` and `**` on numpy arrays
(i.e., vectors and matrices), results in elementwise operations.
This is different from MATLAB, where, for example, `*` will perform a matrix
multiplication.
In order to perform an elementwise operation, your operands must be two array
of compatible sizes, or an array and a scalar.
So, the following elementwise operations are legal:
```python
import numpy as np
A = np.array([[1., 2.], [3., 4.], [5., 6.]])
B = np.array([[13., 14.], [15., 16.], [17., 18.]])
print(f"A+B: {A+B}")
print(f"B*A: {B*A}")
print(f"A-3: {A-3}")
print(f"1./A: {1./A}")
```
This prints:
```
A+B: [[14. 16.]
 [18. 20.]
 [22. 24.]]
B*A: [[ 13.  28.]
 [ 45.  64.]
 [ 85. 108.]]
A-3: [[-2. -1.]
 [ 0.  1.]
 [ 2.  3.]]
1./A: [[1.         0.5       ]
 [0.33333333 0.25      ]
 [0.2        0.16666667]]
```

The following elementwise operations are illegal:
```python
import numpy as np
A = np.array([[1., 2.], [3., 4.], [5., 6.]])
u = np.array([1., 2., 3., 4.])
B = np.array([[13., 14.], [15., 16.]])
A+u
A-B
```
This errors with the messages:
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: operands could not be broadcast together with shapes (3,2) (4,) 
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: operands could not be broadcast together with shapes (3,2) (2,2) 
```

### Matrix arithmetic

There are a variety of mathematic operations in NumPy that are specific to
matrices.
_Matrix multiplication_ is performed via the `@` operator:
```python
import numpy as np
A = np.array([[1., 2.], [3., 4.], [5., 6.]])
u = np.array([7., 8.])
print(f"A@u matrix multiplication: {A@u}")
```
This prints:
```
A@u matrix multiplication: [23. 53. 83.]
```

The _transpose_ of a matrix can be taken with the simple `.T` operator:
```python
import numpy as np
A = np.array([[1., 2.], [3., 4.], [5., 6.]])
print(f"Transpose A.T: {A.T}")
```
This prints:
```
Transpose A.T: [[1. 3. 5.]
 [2. 4. 6.]]
```

Finally, the Frobenius norm of a matrix (and the Euclidean norm of a vector)
can be computed with the `np.linalg.norm` function:
```python
import numpy as np
A = np.array([[1., 2.], [3., 4.], [5., 6.]])
u = np.array([7., 8.])
print(f"||A||_F = {np.linalg.norm(A)}")
print(f"||u|| = {np.linalg.norm(u)}")
```
This prints:
```
||A||_F = 9.539392014169456
||u|| = 10.63014581273465
```

### Solving linear systems

While matrixes in NumPy can be inverted with `np.linalg.inv`, it is generally
not advisable to do so.
Instead, one can solve the linear equation `A@u == b` with the `np.linalg.solve`
function:
```python
import numpy as np
A = np.array([[1., 2.], [3., 4.]])
b = np.array([-2, -3])
print(f"inv(A)@b = {np.linalg.solve(A,b)}")
```
This prints:
```
inv(A)@b = [ 1.  -1.5]
```

### Sparse matrices

When dealing with very large matrices where most entries are zero, it is usually
advisable to _not_ use a `np.array`.
A normal `np.array` stores every single entry of the matrix, wasting a lot of
memory for just zeros.
In the case where we know that a matrix consists mostly of zeros, we want to
use a _sparse matrix_ instead.

SciPy has many sparse matrix formats and many ways to define them.
The simplest, in my opinion, is to use _triplets_:
With triplets, we specify all entries of a matrix that are nonzero in three
lists: the row, the column, and the value.
Given three arrays `i`, `j`, `k` of equal length $n$,
$$A(i[o],j[o]) = k[o] \quad\quad \forall o = 1, \dots, n$$

We construct a matrix from these triplet lists like this:
```python
import numpy as np, scipy as sp
i = np.array([0,1,1,2])
j = np.array([0,1,2,2])
k = np.array([1., -1., -2., 1.])
A = sp.sparse.csr_matrix((k, (i,j)), shape=(3,3)) #the shape tuple is the dimension of A
print(f"A = {A.todense()}")
```
This prints:
```
A = [[ 1.  0.  0.]
 [ 0. -1. -2.]
 [ 0.  0.  1.]]
```
(`toarray()` is a conversion to a dense numpy array for visualization purposes.
Do not do this for large sparse matrices -- this will allocate a giant matrix.)

Sparse matrices can be added and subtracted from each other with `+` and `-`.
They can be multiplied with and divided by scalars with `*` and `/`.
Matrix multiplications are performed with `*`:
```python
import numpy as np, scipy as sp
i = np.array([0,1,1,2])
j = np.array([0,1,2,2])
k = np.array([1., -1., -2., 1.])
A = sp.sparse.csr_matrix((k, (i,j)), shape=(3,3))
i = np.array([0,0,1,2])
j = np.array([0,1,2,1])
k = np.array([-2., -1., 2., 1.])
B = sp.sparse.csr_matrix((k, (i,j)), shape=(3,3))
print(f"A+B = {(A+B).todense()}")
print(f"A*B = {(A*B).todense()}")
```
This prints:
```
A+B = [[-1. -1.  0.]
 [ 0. -1.  0.]
 [ 0.  1.  1.]]
A*B = [[-2. -1.  0.]
 [ 0. -2. -2.]
 [ 0.  1.  0.]]
```

_NOTE: While this is very confusing, in the SciPy world the asterisk `*` denotes
a matrix product if a sparse matrix is involved, and not an elementwise
operation.
SciPy's [sparse arrays](https://docs.scipy.org/doc/scipy/tutorial/sparse.html)
are intended to replace sparse matrices, and they function just like NumPy's
arrays.
However, many libraries (such as Gpytoolbox) still operate with SciPy sparse
matrices, and not sparse arrays._

To solve a sparse linear system `A*x == b` (you should definitely never
explicitly invert a sparse matrix), you can use `sp.linalg.sparse.spsolve`:
```python
import numpy as np, scipy as sp
i = np.array([0,1,1,2])
j = np.array([0,1,2,2])
k = np.array([1., -1., -2., 1.])
A = sp.sparse.csr_matrix((k, (i,j)), shape=(3,3))
b = np.array([-1., 2., 1.])
print(f"inv(A)*b = {sp.sparse.linalg.spsolve(A,b)}")
```
This prints:
```
inv(A)*b = [-1. -4.  1.]
```

Solving a sparse linear system is expensive, but parts of the computation can
be reused if you repeatedly want to solve a system with the same matrix, but
different right-hand sides, like `inv(A)*b`, `inv(A)*c`, `inv(A)*d`, etc.
This is called _precomputation_ or _decomposition_: the matrix `A` is decomposed
once, and the result can be used to solve for different right-hand sides
efficiently.
We first decompose the matrix `A` with `precomp = sp.sparse.linalg.splu(A)`, and we can
then solve for differend right-hand sides with `precomp.solve(rhs)`:
```python
import numpy as np, scipy as sp
i = np.array([0,1,1,2])
j = np.array([0,1,2,2])
k = np.array([1., -1., -2., 1.])
A = sp.sparse.csr_matrix((k, (i,j)), shape=(3,3))
precomp = sp.sparse.linalg.splu(A)
b = np.array([-1., 2., 1.])
print(f"inv(A)*b = {precomp.solve(b)}")
c = np.array([3., 1., -1.])
print(f"inv(A)*c = {precomp.solve(c)}")
d = np.array([1., 1., -2.])
print(f"inv(A)*d = {precomp.solve(d)}")
```
This prints:
```
inv(A)*b = [-1. -4.  1.]
inv(A)*c = [ 3.  1. -1.]
inv(A)*d = [ 1.  3. -2.]
```

That was our linear algebra refresher.
While NumPy and SciPy are extremely powerful libraries with much functionality,
the few operations discussed here cover most of what we will use in basic
geometry processing.

## Other linear algebra libraries

NumPy is not the only python linear algebra library.
Especially if you work in machine learning, you might encounter the popular
[PyTorch](https://pytorch.org) and [jax](https://jax.readthedocs.io/en/latest/)
linear algebra libraries.
These enable you to perform linear algebra computations on the GPU, and add
sophisticated differentiation machinery that can be used for many applications.

These libraries' data structures are not compatible with Gpytoolbox.
You need to convert to and from NumPy in order to use Gpytoolbox with PyTorch
or jax.

For PyTorch, conversions from NumPy to PyTorch and PyTorch to NumPy look like
this:
```python
import numpy as np
import torch
u = np.array([1., 2.])
print(f"array u={u} has type {type(u)}")
ut = torch.from_numpy(u)
print(f"array ut={ut} has type {type(ut)}")
un = ut.numpy()
print(f"array un={un} has type {type(un)}")
```
This prints:
```
array u=[1. 2.] has type <class 'numpy.ndarray'>
array ut=tensor([1., 2.], dtype=torch.float64) has type <class 'torch.Tensor'>
array un=[1. 2.] has type <class 'numpy.ndarray'>
```

jax conveniently mirrors large parts of NumPy and thus feels extremely familiar
to it (although you have to be careful - there are a few subtle differences).
For jax, conversions from NumPy to jax and jax to Numpy look like this:
```python
import numpy as np
import jax
u = np.array([1., 2.])
print(f"array u={u} has type {type(u)}")
uj = jax.numpy.array(u)
print(f"array uj={uj} has type {type(uj)}")
un = np.array(uj)
print(f"array un={un} has type {type(un)}")
```
This prints:
```
array u=[1. 2.] has type <class 'numpy.ndarray'>
array uj=[1. 2.] has type <class 'jaxlib.xla_extension.ArrayImpl'>
array un=[1. 2.] has type <class 'numpy.ndarray'>
```

## That's it!

Our next exercise, [exercise_02](../exercise_02), will be the first one to
actually feature geometry processing.


---

_Oded Stein 2024. [Geometry Processing Research in Python](https://github.com/odedstein/geometry-processing-research-in-python)_

