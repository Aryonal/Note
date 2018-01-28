# Numpy
Before all:
```python
import numpy as np
```

### Array
Generate an array
```python
a = np.array([1,2,3,4], dtype=np.int32)
b = np.zeros((2,2))
c = np.ones((3,3))
d = np.full((4,4), .7) # fill a 2darray with .7
print b.shape # (2,2) (row, col)
```

#### 1.Indexing
just like what's in Matlab, but without `end`
```python
## a[number or list of number]
raw_r0 = b[0,:]     # [0, 0, 0]
raw_r1 = b[1:2, :]  #[[0, 0, 0]]
raw_r2 = b[[2], :]  #[[0, 0, 0]]
print raw_r0.shape  # (3, )
print raw_r1.shape  # (1,3)
print raw_r2.shape  # (1,3)

a = np.array([[1,2,3],[4,5,6],[7,8,9],[10,11,12]])
print a[[0,1,2],[0,1,2]]  # [1,5,9]
```
`arr[lst0, lst1]` means:
```python
# a = arr[lst0, lst1]
a = [arr[lst0[i],lst1[i] for i in xrange(len(lst0))]
```
and bool Indexing

```python

a = np.array([1,2],[3,4],[5,6])
bool_idx = (a > 2)                 #[[False False]
                                   # [True  True]
                                   # [True  True]]
print a[bool_idx]                  #[3 4 5 6]
print a[a > 2]                     #[3 4 5 6]
```

#### 2.Arithmetics
\+ \- \* \/<br>
np.dot() or a.dot(b) for vector a and b

### Matrix
Matrix in num.py is different from array.
```python
a = np.array([1, 2, 3])
b = np.mat(a)

print type(a) #<type 'numpy.ndarray'>
print type(b) #<class 'numpy.matrixlib.defmatrix.matrix'>
```
#### 1. Basic mat processing
Create a mat:
```python
# np.mat(list)
m = np.mat([1,2,3])
m = np.mat([[1,2],[3,4],[5,6]])
# np.mat(ndarray)
m = np.mat(np.zeros((3,3)))               # 3*3 zero mat
m = np.mat(np.ones((2,4)), dtype=None)    # 2*4 ones mat, not identity mat
m = np.mat(np.random.rand(2,2))           # 2*2 rand mat, members are float64 between 0, 1
m = np.mat(np.random.randint(2,8,size=(2,5))) # 2*5 rand mat, members are int between 2, 8
m = np.mat(np.eye(2,2,dtyp=int))          # 2*2 identity mat
m = np.mat(np.diag(np.array([1,2,3])))    # diagonal mat

print m.size                              # mat size, return row*col
print m.shape                             # mat shapre, return (row, col)
```
Arithmetics:
```python
a = np.mat([1,1])
b = np.mat([[1],[2]])

print a.I                   # inverse of a
print a.T                   # teanspose of a
print a.H                   # conjugate transpose
print a.A                   # 2darray of a

print np.add(a,b)           # same as a + b
print np.add(a,-b)          # same as a - b
print np.multiply(a, b)     # same as a * b
print np.cross(a,b)         # a cross b
print a * 2                 # a * 2
```
Indexing:
```python
m = np.mat(np.random.rand(5,5))

print m[:,2:]               # sub mat of m, col 2 to end, row beg to end
print m.max()               # max member
print np.max(m[:,1])        # max member of sub mat
print np.max(m, 0)          # max member of each col, return 1*col mat, same with m.max(0)
print np.max(m, 1)          # max member of each row, return row*1 mat, same with m.max(1)

# replace max with argmax getting the index of maxmember, return type is int or array of int
print m.argmax()            # index of maxmember, return int
print np.argmax(m, 0)       # index of max member in each col, return 1*col mat
```
Combination:
```python
a = np.mat(np.ones((2,2)))
b = np.mat(np.eye(2))
print np.vstack((a,b))          # create 4*2 mat
print np.hstack((a,b))          # create 2*4 mat
```
