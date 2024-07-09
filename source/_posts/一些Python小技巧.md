---
title: 一些Python小技巧
date: 2019-08-19
categories: Python
---

## 1. 进制格式化输出

代码：

```python
print("bin:{:6b},{:6b},{:6b},{:6b}".format(2, 4, 8, 16))
print("oct:{:6o},{:6o},{:6o},{:6o}".format(2, 4, 8, 16))
print("dec:{:6d},{:6d},{:6d},{:6d}".format(2, 4, 8, 16))
print("hex:{:6x},{:6x},{:6x},{:6x}".format(2, 4, 8, 16))
```

输出：

```
bin:    10,   100,  1000, 10000
oct:     2,     4,    10,    20
dec:     2,     4,     8,    16
hex:     2,     4,     8,    10
```

## 2. 位置参数和关键字参数

代码：

```python
def test_tuple(*args):
    # *args 代表一个元组类型，接受位置参数
    print(args)
    result = 0
    for arg in args:
        result += arg
    return result

def test_dict(**kwargs):
    # **kwargs 代表一个字典类型，接受关键字参数
    print(kwargs)
    result = ""
    for arg in kwargs:
        result += arg
    return result

print(test_tuple(1, 2, 3, 4))
print(test_dict(m=1, n=2))
```

输出：

```
(1, 2, 3, 4)
10
{'m': 1, 'n': 2}
mn
```

## 3. 映射转换

代码：

```python
print(list(map(ord, "0123456789\0abcd\0编程喵(●'◡'●)"))) # 提取每一个字符的 Unicode 值
```

输出：

```
[48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 0, 97, 98, 99, 100, 0, 32534, 31243, 21941, 40, 9679, 39, 9697, 39, 9679, 41]
```

## 4. 皮卡丘~

代码：

```python
# `'` 或 `"` 不能包含换行符
print("""
　　 へ　　　　　／|
　　/＼7　　　 ∠＿/
　 /　│　　 ／　／
　│　Z ＿,＜　／　　 /`ヽ
　│　　　　　ヽ　　 /　　〉
　 Y　　　　　`　 /　　/
　ｲ●　､　●　　⊂⊃〈　　/
　()　 へ　　　　|　＼〈
　　>ｰ ､_　 ィ　 │ ／／
　 / へ　　 /　ﾉ＜| ＼＼
　 ヽ_ﾉ　　(_／　 │／／
　　7　　　　　　　|／
　　＞―r￣￣`ｰ―＿　
""")
```

输出：

```
　　 へ　　　　　／|
　　/＼7　　　 ∠＿/
　 /　│　　 ／　／
　│　Z ＿,＜　／　　 /`ヽ
　│　　　　　ヽ　　 /　　〉
　 Y　　　　　`　 /　　/
　ｲ●　､　●　　⊂⊃〈　　/
　()　 へ　　　　|　＼〈
　　>ｰ ､_　 ィ　 │ ／／
　 / へ　　 /　ﾉ＜| ＼＼
　 ヽ_ﾉ　　(_／　 │／／
　　7　　　　　　　|／
　　＞―r￣￣`ｰ―＿　
```

## 5. 类型标注

```python
def f(*x: int):
    print(x)

def g(x: tuple[int, ...]):
    print(x)

def h(x: list[int, any, ...]):
    print(x)

f(1, 2, 3)
g((1, 2, 3))
h([1, "1", 1.0])
```

输出：

```
(1, 2, 3)
(1, 2, 3)
[1, '1', 1.0]
```

## 6. 列表生成

代码：

```python
print([2**n for n in range(21) if 2**n > 1000]) # In Haskell: [2^n | n <- [0 .. 20], 2^n > 1000]
```

输出：

```
[1024, 2048, 4096, 8192, 16384, 32768, 65536, 131072, 262144, 524288, 1048576]
```

## 7. 模式匹配

代码：

```python
status = 418
match status:
    case 400:
        print("Bad request")
    case 404:
        print("Not found")
    case 418:
        print("I'm a teapot")
    case _:
        print("Others")
```

输出：

```
I'm a teapot
```
