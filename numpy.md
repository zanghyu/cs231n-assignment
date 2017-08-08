# 常用函数及成员变量
## numpy.shape
函数形式为

```
ndarray.shape
```

numpy.array类型的数组有shape变量，代表该数组的结构(一个关于该数array的维度的元组)

```
>>>X_train = [[1,2,3],[2,3,4]]
>>>X_train = np.array(X_train)
>>>print X_train.shape
(2,3)
```

numpy也有shape函数，与shape变量结果一致

```
>>>np.shape(X_train)
(2,3)
```

如果只想读取某一维度的长度，则可以

```
>>>X_train.shape[0]
2
```

需要注意的一点是，与如下形式做区分：

```
>>>X_train[0].shape
(3,)
```

## enumerate和numpy.ndenumerate
函数形式为

```
numpy.ndenumerate(arr)
```

enumerate是python的内置函数，当一个列表既需要遍历索引又需要遍历元素时，传统写法是

```
>>>list1 = [1, 2, 3, 4]
>>>for i in range (len(list1)):
...    print i ,list1[i]
0 1
1 2
2 3
3 4
```

比较pythonic的写法是用enumerate,enumerate还可以接收第二个参数，用于指定索引起始值，如：

```
>>>list1 = [1, 2, 3, 4]
>>>for index,item in enumerate(list1,1):
...    print idex,item
1 1
2 2
3 3
4 4
```

numpy.ndenumerate用法与enumerate类似，但是无法指定索引起始值。

```
>>> a = np.array([[1, 2], [3, 4]])
>>> for index, x in np.ndenumerate(a):
...     print(index, x)
(0, 0) 1
(0, 1) 2
(1, 0) 3
(1, 1) 4
```

## numpy.flatnonzero
函数形式为

```
numpy.flatnonzero(a)
```

首先将数组压缩成一行，然后返回其中非0位置，等效于a.ravel().nonzero()[0]

```
>>>X = [[1,2,0,4,5],[2,3,4,0,6]]
>>>X = np.array(X)
>>>print X.ravel().nonzero()[0]
[0 1 3 4 5 6 7 9]
>>>print np.flatnonzero(X)
[0 1 3 4 5 6 7 9]
```

## numpy.random.choice
函数形式为

```
numpy.random.choice(a, size=None, replace=True, p=None)
```

在a中选取size个数，是否可以重复，选取的概率各是多少

```
>>> aa_milne_arr = ['pooh', 'rabbit', 'piglet', 'Christopher']
>>> np.random.choice(aa_milne_arr, 5, p=[0.5, 0.1, 0.1, 0.3])
array(['pooh', 'pooh', 'pooh', 'Christopher', 'piglet'],
      dtype='|S11')
```

## numpy.reshape
函数形式为

```
numpy.reshape(a, newshape, order='C')
```
将a改变为形状是newshape的数组

如果想要某个ndarray的第一维不变，其余维变为一行，可以采用如下形式

```
>>>X_train = np.reshape(X_train, (X_train.shape[0], -1))
```

## numpy.array_split
函数形式为

```
numpy.array_split(ary, indices_or_sections, axis=0)
```

将数组分为若干组

```
>>>X_train = np.array([1,2,3,4,5,6,7])
>>>print np.array_split(X_train,4)
[array([1, 2]), array([3, 4]), array([5, 6]), array([7])]
```

## numpy.argmax和numpy.argsort
函数形式为

```
numpy.argmax(a, axis=None, out=None)
numpy.argsort(a, axis=-1, kind='quicksort', order=None)
````

argmax返回数组中最大值的索引值
argsort返回数组从小到大的索引值

```
>>> x = np.array([3, 1, 2])
>>> np.argsort(x) #按升序排列
array([1, 2, 0])
>>> np.argsort(-x) #按降序排列
array([0, 2, 1])

>>> x[np.argsort(x)] #通过索引值排序后的数组
array([1, 2, 3])
>>> x[np.argsort(-x)]
array([3, 2, 1])
```

## numpy.vstack

函数形式为

```
numpy.vstack(tup)
```

作用为垂直组合多个数组

```
>>>X_train = np.array([[1,2],[3,4],[5,6]])
>>>X_train_folds = np.array_split(X_train,3)
>>>for i in xrange(3):
···    X_train_ = np.vstack(X_train_folds[0:i]+X_train_folds[i+1:])
···    print X_train_
[[3 4]
 [5 6]]
[[1 2]
 [5 6]]
[[1 2]
 [3 4]]
```

