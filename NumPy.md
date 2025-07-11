#ml #ai #python #math #dev 

Python library for creating and manipulating **matrices**, the main data structure used by ML algorithms.

- Python calls matrices *lists*, NumPy calls them *arrays* and TensorFlow calls them *tensors*.

```bash
# download python stable version from python.org
pip3 install numpy
```

#### To create arrays with specific numbers.

```python
import numpy as np

oneD_arr = np.array([1,2,3,4,5])
# [1 2 3 4 5]

twoD_arr = np.array([[1,2,3], [4,5,6]])
# [[1 2 3]
#  [4 5 6]]
```

#### To populate an array with all zeroes, call `np.zeros`. To populate an array with all ones, call `np.ones`.

```python
zeroes_arr = np.zeros(4)
# [0. 0. 0. 0.]

ones_arr = np.ones((3,2))
# [[1. 1.]
#  [1. 1.]
#  [1. 1.]]
```

#### To populate array with a sequence of numbers.

```python
range_arr = np.arange(5, 12)
# [ 5 6 7 8 9 10 11]
```

Notice: upper bound $12$ isn't included.

#### To populate array with random numbers in a range.

```python
random_arr = np.random.randint(low=50, high=101, size=(2,3))
# [[ 80 86 50]
```

Again, upper bound $101$ isn't included.

**Floating Point Integers**

`np.random.random` generates random floats in range $[0, 1]$

```python
noise = np.random.random(5) * 4 - 2
# [ 0.28596444 -1.01168993  1.21450975 -0.68621954 -0.80235151]
```

#### Mathematical Operations

Linear Algebra requires both matrices to be dimensionally compatible. But `numpy` uses a trick called **broadcasting** to expand smaller operands.

```python
range_arr = np.arange(5, 12)
range_arr += 2
# [ 7 8 9 10 11 12 13]

twoD_arr = np.array([[1,2,3], [4,5,6]])
twoD_arr *= 3
# [[ 3  6  9]
# [12 15 18]]
```

