#常用技巧

##截取部分数组

ndarray类型时，可以用如下方式

```
>>>X_train = np.array([1,2,3,4,5,6,7,8,9])
>>>num_training = 5
>>>mask = list(range(num_training))
>>>X_train = X_train[mask]
>>>print X_train
[1 2 3 4 5]
```

##计算l2距离（欧几里得距离）

```
for i in xrange(num_test):
    for j in xrange(num_train):
        dists[i][j] = np.sqrt(np.sum(np.square(X[i]-self.X_train[j])))
```