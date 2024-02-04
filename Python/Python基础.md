# Python基础

## 输出

```python
print(201);

# 写入文件，open("路径","方式")
fp = open('D:/机器学习/python学习/text.txt', 'a+')
print('Hello world', file=fp)
fp.close()
```

## 分支

```python
# 分支 else if
# 判断语句可以写成 60<=grade>=100
# grade = int(input("请输入你的成绩"))
# if 80 <= grade <= 100:
#     print("优秀")
# elif 60 <= grade < 80:
#     print("及格")
# else:
#     print("不及格")

# 条件表达式
# a = int(input("第一个整数"))
# b = int(input("第二个整数"))
# # 比较大小
# # x if 判断条件 else y2
# print(a) if a >= b else print(b)
```

## 变量

```python
# 变量
# 标识 表示对虾所储存的内存地址，使用内置函数id(obj)来获取
# 类型 表示对象的数据类型，使用内置函数type(obj)来获取
# 值 表示对象所存储的具体数据，使用printf(obj)将值打印输出
name = '小李'
nameId = id(name)
nameType = type(name)
print(name, nameId, nameType)

# 多次赋值之后，变量名会指向新的空间
```

## 循环语句

```python
# 循环语句
# while 循环
# a = 1
# while a < 7:
#     if(a % 2 == 0):
#         print(a, "is even")
#     else:
#         print(a, "is odd")
#     a += 1

# for循环
# for letter in 'Python':
#     print(letter)
#
# fruits = ['banana', 'apple', 'mango']
# # for fruit in fruits:
# #     print(fruit)
# for index in range(len(fruits)):
#     print(fruits[index])

# break语句
# for letter in 'python':
#     if letter == 'h':
#         break
#     print(letter)

# continue语句
# for letter in 'python':
#     if letter == 'h':
#         continue
#     print(letter)

# pass 语句
# for letter in 'Python':
#     if letter == 'h':
#         pass
#         print("pass语句")
#     print(letter)
```

## 注释

```python
# 代码注释

# #作为单行注释

# 可以将三引号作为多行注释
"""多行注释
换行"""
```

## 类型

```python
# python 常见的变量类型
# 整数类型、浮点数类型、布尔类型、字符串类型

from decimal import Decimal

name = '小刘';  # str
age = 18;  # int
grade = 95.5;  # float
isBoy = False;  # bool

print(type(name), type(age), type(grade), type(isBoy));

# int
# 二进制以0b开头  八进制以0o开头  十六进制以0x开头


# float
# 浮点数计算结果精度可能不精确，可以通过导入模块decimal进行计算
print(Decimal('1.1') + Decimal('2.2'))

# bool
# True表示真，False表示假（注意要大写）  布尔值可以转换为整数计算
print(True + 1)  # 输出2 真为1，假为0

# str
# 可以使用单引号，双引号和三引号 单和双只能在一行显示，三引号可以分行
str1 = '132'
str2 = "srt2"
str3 = """str3,
换行"""
print(str3)

# 数据类型转换
# str() 将数据类型转换为字符串  int() 将数据类型转换为整数  float() 将其他类型转换为浮点型
# 字符串的小数串（例如：“29.34”）和字符不能转换为int类型
```

## 输入

```python
# input()函数
# 作用：接收来自用户的输入 返回值类型：输入值的类型为str 值的存储：使用=对输入的值进行存储
# 变量名 = input("提示语") 输入的数据会赋值给变量

# 基本使用
# name = input("你的名字是：");
# print(name);

# 高级使用
# 在input中获取int类型
a = int(input("第一个数："))
b = int(input("第二个数："))
print(a + b)
```

## 运算符

```python
# 运算符

# 算数运算符
# 标准运算符（+，-，*，/(除)，//(整除)取整 取余运算符（%）  幂运算符（**）n**m 表示n的m次幂
# // 一正一负的情况下向下取整
print(9 // -4)  # 输出-3
# % 公式：余数=被除数-除数*（商） 针对一正一负的情况

# 赋值运算符
# 执行顺序从右到左
# 支持链式赋值
a = b = c = 20
# 支持参数赋值 += -= /= //= %= /可能会将int类型转换为float
# 支持系列解包赋值 左边要和右边个数一样
d, e, f = 20, 30, 40

print(id(a), id(b), id(c))

# 比较运算符
# >, <, >=, <=, !=, ==(比较的是value) is, is not(比较的是标识)
n = 10
m = 10
print(n is m)  # 结果为True 内存地址相同 但是如果是数组的情况下 内存地址则不相同
arr1 = [11, 12, 13]
arr2 = [11, 12, 13]
print(arr1 is arr2)  # 结果为False

# 布尔运算
# and, or, not, in, not in
# and-->&& or-->|| not-->!
bool1 = False
bool2 = True
print(bool1 or bool2)

str1 = "aldaso"
print('a' in str1)
print('z' in str1)

# 位运算符
# 位与& 对应数位都是1，结果数位才是1，否则为0
# 为或| 对应数位都是0，结果数位才是0，否则为1
# 左移位运算符<< 高位溢出舍弃，低位补0 前一个的两倍
# 右移位运算符>> 低位溢出舍弃，高位补0
print(5 << 4)
print(5 >> 1)

# 运算符的优先级 先算数运算 --> 位运算 --> 比较运算 --> 布尔运算
```