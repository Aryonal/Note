# Numpy
Before all:
```python
import numpy as np
```

### Array

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
