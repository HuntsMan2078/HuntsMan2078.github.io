---
title: Matlab新手教程(1)
date: 2022-10-17 16:28:36
tags:
- Matlab新手教程
categories:
- Matlab
mathjax: true 
---
# Matlab新手教程（1）

## Matlab数据类型
​	Matlab中的数据类型主要包括**数值类型、逻辑类型、字符串、函数句柄、结构体和元胞数组**。下面将分别介绍。

<!-- more -->

### 数值类型：

​	基本的数值类型主要有整数、单精度浮点数和双精度浮点数。需要注意的是，在没有特殊定义的情况下，Matlab对所有数值都按照双精度浮点进行存储和操作。那么为什么要区分这些数值类型呢？这就涉及到精度和内存的矛盾。在工程应用中，我们很多的程序都是在做反复迭代运算，那么双精度浮点数会占用较大的内存，导致程序运行较慢，所以在满足精度要求的条件下，整数类型与单精度浮点数的优点就是节省变量占用的内存空间。

| 数据格式   | 示例 | 说明 |
| :--------: | :--: | :--- |
| int*x*,uint*x* | int32(160) | 有符号和无符号的整数类型；*x*可以为8、16、32、64；**相同数值的整数类型比浮点数类型占用更少的内存**；*需要注意的是*，除了int64和uint64外的所有整数类型，都可以进行数学运算。 |
| single | single(12.4) | 单精度浮点类型；**相同数值的单精度浮点数比双精度浮点数占用更少的内存**；但是单精度浮点数的精度以及能够表示的数值范围比双精度浮点数小。 |
| double | 111.11；     1.000-1.000i | 双精度浮点类型；为Matlab中的默认数值类型。 |

#### 1.整数类型

​	如表格所示，Matlab提供了8种内置的整数类型，分别为有4种有符号*x*位整数**int*x***和4种无符号*x*位整数**uint*x***。这八种整数类型的存储占用位数、能表示的数值范围和转换函数均不相同。具体的数值范围是:
$$
有符号x位整数：-2^{x-1}\sim2^{x-1}-1\\
无符号x位整数：0\sim2^x-1
$$
​	在实际应用中，应根据实际需要合理选择合适的整数类型。由于在Matlab中数值的默认存储类型是双精度浮点数，因此将变量设置为整数类型时，需要使用相依ing的转换函数，即**int*x*/uint*x***，将双精度浮点数转为指定的整数类型。在转换过程中，Matlab默认将待转换数值转换为与之最接近的整数值，若小数部分为0.5，则转换后的结果为与该浮点数最接近的两个整数中绝对值较大的一个。如图所示：

![](https://pic1.imgdb.cn/item/634d077c16f2c2beb1e0bbcd.jpg)

​	另外，这些转换函数也可以将其他数据类型转换为指定的数据类型。在不超出数值范围的情况下，任意两个整数类型之间也可以通过转换函数进行转换。那想必就会有同学思考，既然8位有符号整数类型只能表示-128~127，那如果运算结果超出了其能够表示的范围会怎么样呢？我们可以看到结果是这样的：

![](https://pic1.imgdb.cn/item/634d08be16f2c2beb1e2b7c9.jpg)

​	即当运算结果超出相应的整数类型能够表示的最大范围时，就会出现错误，运算结果被置为该整数类型能够表示的**最大值或最小值**。除了上述命令外，Matlab还包括了几类不同运算法则的取整函数，也可以把浮点数转换成整数。如表：

| 函数FUNC |                        运算法则                         |                   示例                   |
| :------: | :-----------------------------------------------------: | :--------------------------------------: |
| floor(x) |                        向下取整                         |       floor(1.2)=1;floor(-2.5)=-3        |
| ceil(x)  |                        向上取整                         |        ceil(1.2)=2;ceil(-2.5)=-2         |
| round(x) | 取最接近的整数，若小数部分是0.5，则向绝对值大的方向取整 | round(1.2)=1;round(1.5)=2;round(-2.5)=-3 |
|  fix(x)  |                         向0取整                         |    fix(1.2)=1;fix(1.7)=1;fix(-1.7)=-1    |

#### 2.浮点数类型

​	如前所述，Matlab提供了单精度浮点和双精度浮点，其存储位宽、能够表示的数值范围、数值精度各方面都不相同。总体来说，单精度浮点占用位数少，因此占用内存小，但能够表示的数值范围和数值的精度都比双精度浮点小。而且需要注意的是两种浮点数都是有符号数，其最高位是符号位，0正1负。

​	双精度浮点数在参与运算时，返回值的类型依赖于参与运算的其他数据类型。具体如表所示：

| 参与运算的数据类型 | 返回值类型 |
| :----------------: | :--------: |
| 逻辑类型、字符类型 | 双精度浮点 |
|       整数型       |   整数型   |
|     单精度浮点     | 单精度浮点 |

* **注意**：在Matlab中，单精度浮点不能与整数类型进行算术运算。

![](https://pic1.imgdb.cn/item/634d1c4f16f2c2beb1022b43.jpg)

#### 3.复数

​	在Matlab中默认使用i/j作为虚部标志。在创建复数时，可以直接按照复数形式进行输入或者使用*complex*函数。

| 函数         | 说明                       |
| ------------ | -------------------------- |
| real(z)      | 返回复数的实部             |
| imag(z)      | 返回复数的虚部             |
| abs(z)       | 返回复数的模               |
| angle(z)     | 返回复数的辐角             |
| conj(z)      | 返回复数的共轭复数         |
| complex(a,b) | 以a为实部，b为虚部创建复数 |

```matlab
>> a=real(3+4i);%返回实部
>> b=imag(3+4i);%返回虚部
>> c=abs(3+4i);%返回模
>> d=angle(3+4i);%返回辐角
>> e=conj(3+4i);%返回共轭复数
>> f=complex(3,4);%以3，4创建复数
结果为：
>> a,b,c,d,e,f
a =

     3
b =

     4
c =

     5
d =

    0.9273
e =

   3.0000 - 4.0000i
f =
  3.0000 + 4.0000i
```

#### 4.无穷量(Inf)和非数值量(NaN)

​	Matlab中使用Inf和-Inf分别代表正无穷量和负无穷量，NaN表示非数值量。正负无穷量的产生一般是由于运算溢出导致，产生了超出双精度浮点数数值范围的结果；非数值量则是由于*0/0*或者*Inf/Inf*类型的非正常运算而产生的，这两个NaN彼此时不相等的。

```matlab
>> a=0/0,b=log(0),c=inf-inf
a =

   NaN
b =

  -Inf
c =

   NaN
```

​	以上就是Maltab中数据类型的数值类型部分。掌握数值类型能够帮助我们在一些特定场景下选择合适的函数或数值类型，亦可以在程序报错的时候及时发现错误。
