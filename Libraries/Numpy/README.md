To get started: https://scipy-lectures.org/intro/numpy/operations.html

## Array creation methods

### np.array - Create an array from list
Create an array with two rows and three columns.
```Python
a = np.array([[1, 2, 3],[1, 2, 3]])
```

### np.zeros - Create an array with zeros
Create an array containing any number of zeros:
```Python
a = np.zeros(5)
```
**Out**: `array([0., 0., 0., 0., 0.])`

Create a 3 dimensional array:
```Python
a = np.zeros((2,3,4))
```
**Out**:
```
array([[[0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.]],

       [[0., 0., 0., 0.],
        [0., 0., 0., 0.],
        [0., 0., 0., 0.]]])
```

Create a two dimension array with zeros:

```Python
a = np.zeros(2, 3)
```
**Out**: `array([[0., 0., 0.],
       [0., 0., 0.]])`

### np.ones - Create an array with ones
```Python
ones = np.ones((2,3))
```
**Out**: `array([[1., 1., 1.],
       [1., 1., 1.]])`

### np.arange - Create an array in a range
This method looks like python **range()**:
```Python
a = np.arange(10)
```
**Out**: `array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])`

Of course, we can indicate *start*, *end*, *step*:
```Python
a = np.arange(0, 10, 2)
```
**Out**: `array([0, 2, 4, 6, 8])`

### np.linspace - Create an array of spaced numbers
```Python
a = np.linspace(0, 1, 5)
```
**Out**: `array([0.  , 0.25, 0.5 , 0.75, 1.  ])`

### np.eye - Create an identity matrix
```Python
a = np.eye(4)
```
**Out**: `array([[1., 0., 0., 0.],
       [0., 1., 0., 0.],
       [0., 0., 1., 0.],
       [0., 0., 0., 1.]])`

Or like this:
```Python
a = np.zeros((3,4))
```
**Out**: `array([[0., 0., 0., 0.],
       [0., 0., 0., 0.],
       [0., 0., 0., 0.]])`

### np.full - Create an array with a given value
np.full takes a matrix dimension (a shape), a value, and create a matrix full of this value:
```Python
a = np.full((3,4), np.pi)
```
**Out**:
```
array([[3.14159265, 3.14159265, 3.14159265, 3.14159265],
       [3.14159265, 3.14159265, 3.14159265, 3.14159265],
       [3.14159265, 3.14159265, 3.14159265, 3.14159265]])
```

### np.empty - Create an array with unpredictable values
```Python
a = np.empty((2,3))
```
**Out**:
```
array([[1., 1., 1.],
       [1., 1., 1.]])
```


### np.random - Create an array with random values
Others methods exists to create a random arrays !
```Python
a = np.random.random((3,4))
```
**Out**:
```
array([[0.21064871, 0.51084367, 0.04462232, 0.15474993],
       [0.48943545, 0.17311007, 0.6829123 , 0.48621628],
       [0.33423204, 0.84978756, 0.35483656, 0.56232577]])
```

We can also put a seed and then create a randint array:
```Python
np.random.seed(0)
a = np.random.randint(10, size=6)  
```
**Out**:`array([5, 0, 3, 3, 7, 9])`

### np.fromiter - Create an array from an iterator
```def generator():
    i = 0
    
    while True:
        i+= 1
        yield i

arr = np.fromiter(generator(), dtype=int, count=10)
```
**Out**:`array([ 1  2  3  4  5  6  7  8  9 10])`

## Array metadata methods

For the following array:
**Out**: `array([[0., 0., 0., 0.],
       [0., 0., 0., 0.],
       [0., 0., 0., 0.]])`

### Dimension of the matrice - Shape:
```Python
a.shape
# Out: (3, 4)
```

### Number of dimensions - Rank:
```Python
a.ndim
# Out: 2
```

### Size of the matrice:
```Python
a.size
# Out: 12
```

### Type of a numpy array:
```Python
type(np.zeros((2,3,4)))
# Out: numpy.ndarray
```

### Buffer of an array:
```Python
a = np.array([[1,2],[1000, 2000]], dtype=np.int32)
a.data
# Out: <memory at 0x0000016531D6AF28>
```

## Arrays operations

### np.concatenate - Concatenate two arrays
Concatenate two arrays:

```Python
x = np.array([1, 2, 3])
y = np.array([3, 2, 1])
np.concatenate([x, y])
```
**Out**: `array([1, 2, 3, 3, 2, 1])`

### np.vstack & np.hstack - Stack vertically/horizontally
References: [numpy.vstack](https://numpy.org/doc/stable/reference/generated/numpy.vstack.html), [numpy.hstack](https://numpy.org/doc/stable/reference/generated/numpy.hstack.html).

**Vstack**:
```Python
x = np.array([1, 2, 3])
y = np.array([[9, 8, 7], [6, 5, 4]])
np.vstack([x, y])
```
**Out**: `array([[1, 2, 3],
       [9, 8, 7],
       [6, 5, 4]])`

**Hstack**:
```Python
x = np.array((1, 2, 3))
y = np.array((2, 3, 4))
np.hstack([x, y])
```
**Out**: `array([1, 2, 3, 2, 3, 4])`

## NDarray: an homogeneous array
**numpy.ndarray** represents a multidimensional, homogeneous array of fixed-size items.

### dtype - Get the type of items in the ndarray:

With integers:
```Python
a = np.arange(1, 5)
print(a.dtype, a)
# Out: int32 [1 2 3 4]
```

With floating numbers:
```Python
a = np.arange(1.0, 5.0)
print(a.dtype, a)
# Out: float64 [1. 2. 3. 4.]
```

### Specify the dtype on array creation:
Instead of letting NumPy guess what data type to use, we can set it explicitly when creating an array:

With 64 bits complex numbers:
```Python
a = np.arange(1, 5, dtype=np.complex64)
print(a.dtype, a)
# Out: complex64 [1.+0.j 2.+0.j 3.+0.j 4.+0.j]
```

Available data types include int8, int16, int32, int64, uint8|16|32|64, float16|32|64 and complex64|128. Check out [the documentation](https://numpy.org/doc/stable/reference/arrays.dtypes.html) for the full list, and [here too](https://numpy.org/doc/stable/user/basics.types.html).


### itemsize - Get the size in bytes (octets) of each item:
Here we have 64bits numbers, so 8 bytes/octets numbers:
```Python
a = np.arange(1, 5, dtype=np.complex64)
a.itemsize
# Out: 8
```

## Arrays operations:

For a given array:
```Python
x1 = np.random.randint(10, size=6)  
```

### Get the first n-elements of an array:
```Python
print(x1[:5])
# Out: [5 0 3 3 7]
```

### Print the elements from the 6th and on:
```Python
print(x1[5:]) 
# Out: [9]
```

### Print every thwo elements of an array:
```Python
print(x1[::2])
# Out: [5 3 7]
```

## Arithmeric operations
All the usual arithmetic operators (+, -, , /, //, *, etc.) can be used with ndarrays. They apply elementwise:
```Python
a = np.array([14, 23, 32, 41])
b = np.array([5,  4,  3,  2])

print("a + b  =", a + b)
print("a - b  =", a - b)
print("a * b  =", a * b)
print("a / b  =", a / b)
print("a // b  =", a // b)
print("a % b  =", a % b)
print("a ** b =", a ** b)
```

For additions/substractions, if the arrays have not the same dimensions, **Python will raise a ValueError**.
For multiplications/divitions, if column number of a does not match the line number of b, **Python will raise a ValueError**.

### Matrix mumtiplication by a single value
All the values are multiplied by 2:
```Python
C = A * 2 
```

### Mulltiply two matrices - ndarray.dot
The number of columns of A must correspond to the number of rows of B:
```Python
C = A.dot(B)
```

### Avoid ValueError in multiplication: Transpose
Transposing a matrice (array) = "turn" its shape vertically -> horizontally.

B.transpose() can be written B.T
```Python
B = np.array([[1,2,3],[4,5,6]])
BT = B.T
```
**Out**: `[[1 4]
 [2 5]
 [3 6]]`
