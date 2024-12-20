---
title: Matlab新手教程(3)
date: 2022-10-24 21:43:51
tags:
- Matlab新手教程
categories:
- Matlab
mathjax: true
---

​	在[Matlab新手教程(2)](https://huntsman.link/2022/10/19/Matlab%E6%96%B0%E6%89%8B%E6%95%99%E7%A8%8B(2)/)中，我们学习了Matlab数据类型中的逻辑类型、字符和字符串类型以及函数句柄类型，今天将要学习一个比较难理解但是很有用的数据类型：**元胞数组**。

<!-- more -->

# 数组

​	在Matlab中进行运算的所有数据类型，都是按照数组及矩阵的形式进行存储和运算的，二者在Matlab中的剧本运算性质不同，数组强调<u>元素对元素的运算</u>，而矩阵则采用<u>线性代数的运算方式</u>。我们先介绍一下数组，数组的属性及数组之间的逻辑关系，是编写程序时非常重要的两个方面。在Matlab平台上，数组的定义是广义的，它的元素可以是任何数据类型，比如我们先定义一个最基本的数组：

```matlab
>> a=[1,2,3]

a =

     1     2     3
```

​	那如果我们需要定义很多个相同步长元素的数组，我们可以使用冒号*:*来代表一系列数值，在没有指定步长前Matlab默认步长为1。

```matlab
>> a=1:10

a =

     1     2     3     4     5     6     7     8     9    10
```

​	那么我们给出创建一个数字数组的最一般形式

```matlab
Array = i:j:k
```

​	创建从i开始，步长为j，到k结束的数字数组。如果i>k，则Matlab会返回一个空矩阵，例如

```matlab
>> a=1:0.5:10

a =

  列 1 至 6

    1.0000    1.5000    2.0000    2.5000    3.0000    3.5000

  列 7 至 12

    4.0000    4.5000    5.0000    5.5000    6.0000    6.5000

  列 13 至 18

    7.0000    7.5000    8.0000    8.5000    9.0000    9.5000

  列 19

   10.0000
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
>> a=10:0.5:1

a =

  空的 1×0 double 行向量
```

​	Matlab中还预定义了一些函数也可以用来创建线性序列和逻辑序列比如：linspace(a,b,n)

```
%在区间[a,b]上创建一个有n个元素的向量
>> a=linspace(0,5,6)%采用linspace创建

a =

     0     1     2     3     4     5

>> b=0:1:5%采用步长形式创建

b =

     0     1     2     3     4     5

>> isequal(a,b)%判断a与b是否相等

ans =

  logical

   1
```

# 元胞数组

​	介绍完了基本数组，我们就要开始学习元胞数组，元胞数组是一种无所不包的广义矩阵，你可以理解为这个矩阵的每一个元素可以是Matlab数据类型中的任意一种，甚至你可以套娃，在一个元胞数组内嵌套多个元胞数组。所以我比较喜欢把它定义为一个收纳箱，这个收纳箱里面可以装任何东西，而且它的维数也不受限制，可以是一维二维乃至多维，所以在元胞数组中元素不称为元素，而是**元胞**。

## 元胞数组的创建

​	那么我们该如何创建一个元胞数组呢？Matlab里面提供了两种方法，第一种方法是通过赋值语句进行创建，第二种方法是通过cell函数创建空元胞数组然后进行赋值。我们先尝试第一种方法：通过赋值语句进行创建，这里需要注意的是，**与普通数组有所不同，元胞数组使用花括号{}进行创建，使用逗号，分隔每一个单元，使用分号；换行。**

```matlab
>> a = {'huntsman',[2,0,7,8];'is','nice'}%创建元胞数组a

a =

  2×2 cell 数组

    {'huntsman'}    {1×4 double}
    {'is'      }    {'nice'    }
    
>> celldisp(a)%显示元胞数组a
 
a{1,1} =
 
huntsman
 
 
a{2,1} =
 
is
 
 
a{1,2} =
 
     2     0     7     8

 
 
a{2,2} =
 
nice
```

​	接下来我们采用cell函数创建

```matlab
%cell函数的调用格式为：cellName = cell(m,n)，创建一个m*n行的元胞数组，其每一个单元均为空
>> b=cell(2,2)

b =

  2×2 cell 数组

    {0×0 double}    {0×0 double}
    {0×0 double}    {0×0 double}
```

## 元胞数组的寻访

​	**WARNING**：<u>元胞数组的寻访</u>！！！关于Matlab逻辑底层对于元胞内和元胞外寻址这里不做赘述，我们只需要理解元胞数组对应的操作对象有两个，一个元胞数组中的单元，一个是元胞数组单元中的内容。

**重要的内容读三遍**

**重要的内容读三遍**

**重要的内容读三遍**

对于元胞数组C来说，C(m,n)指的是元胞数组中第m行n列，而C{m,n}指的是元胞数组中第m行n列中的内容。下面我们通过代码来分析他们的不同。我们还是以刚刚定义的2x2元胞数组a来举例：

```matlab
>> b=a(1,1)%对元胞数组单元进行操作

b =

  1×1 cell 数组

    {'huntsman'}

>> c=a{1,1}%对元胞数组单元内容进行操作

c =

    'huntsman'
 
>> whos b
  Name      Size            Bytes  Class    Attributes

  b         1x1               120  cell               

>> whos c
  Name      Size            Bytes  Class    Attributes

  c         1x8                16  char               
```

​	观察b和c的class，我们发现b是cell也就是元胞数组，而c是char也就是字符串，希望通过这个例子大家能分清这两个操作的不同。

## 元胞数组的操作

​	元胞数组的操作包括合并、删除元胞数组中的指定单元、改变元胞数组的形状等。我们将依次介绍。

### 元胞数组的合并

​	所谓元胞数组的合并，其实就是我们先对元胞数组单元中的内容赋值，然后组成一个元胞数组，就类似于我们造车的时候先把轮胎、座椅等等部件造好，然后将其组合也就成为了一台车。而不是先把车架做好，再一个一个部件安上去。

```matlab
>> a{1,1}='huntsman';
a{1,2}='is';
a{1,3}='nice';
>> a

a =

  1×3 cell 数组

    {'huntsman'}    {'is'}    {'nice'}
```

### 元胞数组中指定单元的删除

​	这个部分很好理解，我们要删除指定单元中的内容，我们只需要将其赋值为空矩阵即可，但是要注意的的是我们操作的对象是内容。

```matlab
>> a(1,1)=[]%操作对象不正确，报错
空赋值只能具有一个非冒号索引。
 
>> a{1,1}=[]%赋值空矩阵

a =

  1×3 cell 数组

    {0×0 double}    {'is'}    {'nice'}
```

### 使用reshape函数改变元胞数组的形状

​	reshape函数的调用格式为：

```matlab
trimC = reshape(C,M,N)
```

​	表示将元胞数组C改变成M行N列的新元胞数组。

```matlab
>> C = cell(3,4)

C =

  3×4 cell 数组

    {0×0 double}    {0×0 double}    {0×0 double}    {0×0 double}
    {0×0 double}    {0×0 double}    {0×0 double}    {0×0 double}
    {0×0 double}    {0×0 double}    {0×0 double}    {0×0 double}

>> newC = reshape(C,4,3)

newC =

  4×3 cell 数组

    {0×0 double}    {0×0 double}    {0×0 double}
    {0×0 double}    {0×0 double}    {0×0 double}
    {0×0 double}    {0×0 double}    {0×0 double}
    {0×0 double}    {0×0 double}    {0×0 double}
```

# 本节小结

本节我们学习了Matlab数据结构中的数组，尤其需要掌握的是元胞数组，因为元胞数组就像一个收纳盒一样，或者像一个RAM一样，我们可以把我们需要的东西存到元胞数组中，方便地取用。在下一节中，我们开始学习结构体。