# NumPy Python Library
<p align="center">
  <img src="../images/Numpy.png" alt="NumPy Diagram" width="600">
</p>
NumPy is a core Python library for numerical computing, built for
handling large arrays and matrices efficiently. It is significantly
faster than Python's built-in lists because it uses optimized C-style
storage where actual values are stored at contiguous memory locations
(not object references). It also supports **vectorized computations**.

## Key Features

- **ndarray object**: Stores homogeneous data in n-dimensional arrays
  for fast processing.
- **Vectorized operations**: Perform element-wise calculations without
  explicit loops.
- **Broadcasting**: Apply operations across arrays of different shapes.
- **Linear algebra functions**: Matrix multiplication, inversion,
  eigenvalues, etc.
- **Statistical tools**: Mean, median, standard deviation, and more.
- **Fourier transforms**: Fast computation for signal and image
  processing.
- **Integration with other libraries**: Works seamlessly with Pandas,
  SciPy, and scikit-learn.

> **Note** - NumPy arrays are **homogeneous**, meaning all elements must
> be the same data type. - Vectorized operations in NumPy can be
> **10--100× faster** than Python loops.

------------------------------------------------------------------------

## What is NumPy Used For?

With NumPy, you can perform a wide range of numerical operations,
including:

- Creating and manipulating arrays
- Performing element-wise and matrix operations
- Generating random numbers and statistical calculations
- Conducting linear algebra operations
- Working with Fourier transformations
- Handling missing values efficiently

------------------------------------------------------------------------

## Why Learn NumPy?

- Faster math operations on large datasets
- Cleaner code without complex loops
- Built-in functions for statistics and algebra
- Foundation for Pandas, SciPy, TensorFlow, and more
- Efficient memory usage

------------------------------------------------------------------------

# Different Ways to Create NumPy Arrays in Python

Creating NumPy arrays is a fundamental aspect of working with numerical
data in Python. NumPy provides various methods to create arrays
efficiently, catering to different needs and scenarios.

## Create NumPy Arrays Using Lists or Tuples

The simplest way to create a NumPy array is by passing a Python list or
tuple to the `numpy.array()` function. This method creates a
one-dimensional array.

    import numpy as np

    my_list = [1, 2, 3, 4, 5]
    numpy_array = np.array(my_list)

    print("Simple NumPy Array:", numpy_array)

**Output**

    Simple NumPy Array: [1 2 3 4 5]

------------------------------------------------------------------------

## Initialize Arrays Using Special Functions

NumPy provides several built-in functions to generate arrays with
specific properties.

- `np.zeros()` -- Creates an array filled with zeros
- `np.ones()` -- Creates an array filled with ones
- `np.full()` -- Creates an array filled with a specified value
- `np.arange()` -- Creates an array with evenly spaced values within a
  range
- `np.linspace()` -- Creates an array with evenly spaced values over a
  specified interval

<!-- -->

    import numpy as np

    zeros_array = np.zeros((2, 3))
    ones_array = np.ones((3, 3))
    constant_array = np.full((2, 2), 7)
    range_array = np.arange(0, 10, 2)  # start, stop, step
    linspace_array = np.linspace(0, 1, 5)  # start, stop, num

    print(zeros_array)
    print(ones_array)
    print(constant_array)
    print(range_array)
    print(linspace_array)

  


------------------------------------------------------------------------

## Random Number Generation

NumPy provides functions to create arrays filled with random numbers.

- `np.random.rand()` -- Uniform distribution over \[0, 1)
- `np.random.randn()` -- Standard normal distribution
- `np.random.randint()` -- Random integers within a given range

<!-- -->

    import numpy as np

    random_array = np.random.rand(2, 3)
    normal_array = np.random.randn(2, 2)
    randint_array = np.random.randint(1, 10, size=(2, 3))

    print(random_array)
    print(normal_array)
    print(randint_array)

------------------------------------------------------------------------

## Matrix Creation Routines

NumPy provides functions to create specific types of matrices.

- `np.eye()` -- Creates an identity matrix
- `np.diag()` -- Constructs a diagonal array
- `np.zeros_like()` -- Creates an array of zeros with the same shape and
  type as another array
- `np.ones_like()` -- Creates an array of ones with the same shape and
  type as another array

<!-- -->

    import numpy as np

    identity_matrix = np.eye(3)
    diagonal_array = np.diag([1, 2, 3])
    zeros_like_array = np.zeros_like(diagonal_array)
    ones_like_array = np.ones_like(diagonal_array)

    print(identity_matrix)
    print(diagonal_array)
    print(zeros_like_array)
    print(ones_like_array)

------------------------------------------------------------------------

## Video Tutorial

[NumPy Tutorial](https://www.youtube.com/watch?v=VXU4LSAQDSc)
