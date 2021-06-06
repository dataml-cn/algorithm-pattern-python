# Python 快速入门

## 基本语法

[廖雪峰 Python](https://www.liaoxuefeng.com/wiki/1016959663602400/)

## 常用库

### 栈、队列操作

Python 通过list的append、pop操作模拟栈和队列操作
- `append` 最后加入元素
- `pop` 默认弹出最后一个元素, 但也可以指定弹出的下标, 比如把一个元素弹出`pop(0)` 

#### 栈

```python
# create
stack = list()

stack.append(10)

# pop last element
stack.pop()

# check empty
len(stack)==0
```


#### 队列

```python
queue = list()
queue.append(10)
queue.pop(0)
```

**注**

- 也可以通过切片的方式模拟

### 字典

基本用法

```python
# create
map = dict()

# set key
map[key] = value

# get
map.get(key)
map.get(key, default_value)

# delete
map.pop(key)
del map[key]

# for each
for key, value in map.items():
    print(key, value)

# key in dict
if key in map：
    pass

```

### 标准库

#### sort

```python
tmp = [1, 5, 3]
tmp.sort(reverse=False)
# tmp: [1, 3, 5]

tmp = ['ab', 'c', 'ef']
tmp.sort(key=len)
# tmp: ['c', 'ab', 'ef']
```

**注**

- 可以自定义key


#### math

```python
sys.maxsize
```

#### copy

```python
obj_copy = obj.copy()
```

### 常用技巧

类型转换

```python

num_str = "12345"
num = int(num_str) 
new_str = str(num)
```

**注**

- leetcode 中，全局变量不要当做返回值，否则检查器会报错
