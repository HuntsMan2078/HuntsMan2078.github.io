---
title: Matlab新手教程(2)
date: 2022-10-19 15:57:22
tags:
- Matlab新手教程
categories:
- Matlab
mathjax: true
---

# Matlab新手教程（2）

​	在[Matlab新手教程（1）中](https://huntsman.link/2022/10/17/Matlab%E6%96%B0%E6%89%8B%E6%95%99%E7%A8%8B(1)/)，我们介绍了Maltab数据类型中的第一种：数值类型，接下来我们介绍第二种：逻辑类型。

<!-- more -->

## 逻辑类型

​	逻辑类型的数据是指布尔类型的数据及数据之间的逻辑关系。除了传统的数学运算，Maltab还支持关系和逻辑运算。这些运算的目的是提供求解真/假命题的答案。作为所有关系和逻辑表达式的输入，Matlab把任何非零数值当作真，把零当作假。所有关系和逻辑表达式的输出：对于真，输出为1；对于假，输出为0。逻辑类型数据在进行运算时需要用到关系操作符和逻辑运算符，如下表：

| 关系操作符 |    说明    |
| :--------: | :--------: |
|     <      |    小于    |
|     <=     | 小于或等于 |
|     >      |    大于    |
|     >=     | 大于或等于 |
|     ==     |    等于    |
|     ~=     |   不等于   |
|     &      |     与     |
|     \|     |     或     |
|     ~      |     非     |

​	Matlab中的关系操作符能够用来比较两个同样大小的数组，或者用来比较一个数组和一个标量。在后一种情况下，标量会和数组中的每一个元素进行比较，结果与数组大小一样，例如：

```matlab
>> a= 1:5,b=7-a
a =
     1     2     3     4     5
b =
     6     5     4     3     2
>> TrueorFalse = (a == b)%判断a与b中的元素是否相等
TrueorFalse =
  1×5 logical 数组
   0   0   0   0   0%这里我们看到没有元素相等，所以全部返回0
%%--------------------------------------------------------   
>> a=1:10,b=10-a
a =
     1     2     3     4     5     6     7     8     9    10
b =
     9     8     7     6     5     4     3     2     1     0
>> TrueorFalse=(a==b)
TrueorFalse =
  1×10 logical 数组
   0   0   0   0   1   0   0   0   0   0%现在我们看到a与b中的5相等，返回1
```

​	同理，Matlab也可以做逻辑运算，如：

```matlab
>> A = 1:10;
>> TrueorFalse = (A>3)&(A<8)%判断A中元素是否在3~8之间
TrueorFalse =
  1×10 logical 数组
   0   0   0   1   1   1   1   0   0   0
```

​	除了上述关系操作符与逻辑运算符，Matlab还提供了大量其他关系的逻辑函数。

1. ***xor(x,y)***：异或运算，*x*和*y*同时为假或真时返回0，否则返回1；
2. ***any(x)***：判断是否为零向量或零矩阵，如果是非零的，返回1，否则返回0；
    除此之外，Matlab还提供了一些函数，在运算过程中用来测试特殊值或者条件是否存在，并返回相应的表示结果，大家看看就行
    ![](https://pic1.imgdb.cn/item/634fdff516f2c2beb19503b0.jpg)

## 字符和字符串

​	在Matlab中，文本当作特征字符串或者简单地当作字符串。字符串能够显示在屏幕上，也可以用来构成一些命令，这些命令在其他的命令中用于求值或者被执行。

​	在Matlab中可能会遇到对字符和字符串的操作，笔者曾经就遇到过这样的问题，需要对字符进行转码。一个字符串是存储在一个**行向量**中的文本，这个行向量中的每一个元素代表一个字符。实际上，想必大家已经知道了，在Matlab中字符也是以ASCII码存储的。当在屏幕上显示字符变量的值时，显示出来的是文本，而不是ASCII数字。由于字符串是通过向量形式来存储的，因此可以通过对它的下标对字符串中的任何一个元素进行访问。字符矩阵也可以通过下标索引进行访问，但是**矩阵的每行字符数必须相同**。

​	下面我们以一个最简单的例子来说明字符串和ASCII码之间的表达：

```matlab
>> str='huntsman.link is a good web'
str =
    'huntsman.link is a good web'
>> abs(str)
ans =
  列 1 至 19
   104   117   110   116   115   109    97   110    46   108   105   110   107    32   105   115    32    97    32
  列 20 至 27
   103   111   111   100    32   119   101    98
```

​	从以上代码我们可以看到，每一个字符都被转换成了ASCII码，那此时我们就可以对其进行操作，例如我们将所有的字符ASCII码加10

```matlab
>> ASCII=ans+10
ASCII =
  列 1 至 19
   114   127   120   126   125   119   107   120    56   118   115   120   117    42   115   125    42   107    42
  列 20 至 27
   113   121   121   110    42   129   111   108
>> char(ASCII)
ans =
    'rx~}wkx8vsxu*s}*k*qyyn*ol'
```

​	我们再将操作完成后的ASCII码转为文字我们可以发现已经操作成功了。那我们再减10把它变回来。

```matlab
>> ASCII=ASCII-10
ASCII =
  列 1 至 19
   104   117   110   116   115   109    97   110    46   108   105   110   107    32   105   115    32    97    32
  列 20 至 27
   103   111   111   100    32   119   101    98
>> char(ASCII)
ans =
    'huntsman.link is a good web'
```

​	所以我们发现了，因为字符串是数值数组，所以它们可以用Matlab中所有可利用的数组操作工具进行操作。例如，我们继续针对之前定义的字符串进行操作：

```matlab
>> U = str(1:8)
U =
    'huntsman'
```

或者我们可以：

```matlab
>> U=str(8:-1:1)
U =
    'namstnuh'
```

​	所以，在Matlab中字符串像数组一样进行编址。这里再叮嘱一下，字符串中的单引号是通过两个连续的单引号表示的：

```matlab
>> str2='I''m HuntsMan2078'
str2 =
    'I'm HuntsMan2078'
```

​	另外，我们也可以像构建矩阵一样构建一个字符串：

```matlab
>> U='I''m '
>> V='HuntsMan2078';
>> W=[U,V]
W =
    'I'm HuntsMan2078'
```

## 函数句柄

​	在Matlab中，对函数的调用方法分为直接调用和间接调用。	

**直接调用**，被调用的函数成为子函数。但是子函数只能被与其M文件同名的主函数或在M文件中的其他函数所调用，这里大家可以理解为子函数不是一个全局变量，它只在当前程序有用。

**间接调用**，使用函数句柄对函数进行调用可以避免上述的问题。函数句柄提供了一种间接调用函数的方法，。创建函数句柄需要用的操作符*@*。对Matlab库函数中提供的各种M文件中的函数和我们自己编写的程序中的内部函数，都可以创建函数句柄，从而可以通过函数句柄来实现对这些函数的间接调用。

​	创建函数句柄的一般句法格式为：

```matlab
Function_Handle = @Function_Filenmae;
```

​	其中：

* Function_Filename是函数所对应的M文件的名称或Matlab内部函数的名称。

* @是句柄创建操作符。

* Function_Handle变量保存了这一函数句柄，并在后续的运算中作为数据流进行传递。

例如，F_Handle=@cos就创建了Matlab内部函数cos的句柄，并将其保存在F_Handle变量中，在后续的运算过程中就可以通过F_Handle(x)来实现cos(x)的功能。

```matlab
>> F_Handle=@cos;
>> F_Handle(0)
ans =
     1
     
>>F_Handle
F_Handle =
  包含以下值的 function_handle:
    @cos
```

​	在通过函数句柄调用函数时，也需要指定函数的输入参数。如：可以通过F_Handle(arg1,arg2,...,argn)这样的调用格式来调用具有多个输入参数的函数。对于那些没有输入参数的函数，在使用句柄调用时，在句柄变量之后的圆括号中不填写变量名即可，即F_Handle()。Matlab库函数中提供了大量关于处理函数句柄的操作函数，将函数句柄的功能与其他数据类型联系起来，扩展了函数句柄的应用。函数句柄的简单操作函数如表：

| 函数名称                       | 函数功能                                                     |
| ------------------------------ | ------------------------------------------------------------ |
| functions(funhandle)           | 返回一个结构体，存储了函数的名称、函数类型（simple或overload），以及函数M文件的位置 |
| func2str(funhandle)            | 将函数句柄转换为函数名称字符串                               |
| str2func(str)                  | 将字符串代表的函数转换为函数句柄                             |
| save filename.mat funhandle    | 将函数句柄保存在*.mat文件中                                  |
| load filename.mat funhandle    | 吧*.mat文件中存储的函数句柄加载到工作区                      |
| isa(var,'function_handle')     | 检测变量var是否是函数句柄                                    |
| isequal(funhandlea,funhandleb) | 检测两个函数句柄是否对应同一个函数                           |

```matlab
%funstions(funhandle)演示
>> fun_a=@cos
fun_a =
  包含以下值的 function_handle:
    @cos
>> functions(fun_a)
ans = 
  包含以下字段的 struct:
    function: 'cos'
        type: 'simple'
        file: ''

%func2str(funhandle)演示       
>> func2str(fun_a)
ans =
    'cos'
    
%str2func(str) 演示
>> str2func(ans)
ans =
  包含以下值的 function_handle:
    @cos
    
%save filename.mat funhandle/load filename.mat funhandle演示  
>> func_a=@cos;%定义函数句柄func_a
>> save func_a.mat func_a%把函数句柄'func_a'存储成'func_a.mat’文件，注意，文件名可以任取，这时你会发现你的matlab当前工作文件夹中出现了'func_a.mat’文件
>> clear%将工作区中的所有变量清除，然后我们尝试运算一下
>> func_a(pi)
函数或变量 'func_a' 无法识别。%我们发现现在函数句柄不能识别。
>> load func_a.mat func_a%重新载入我们刚刚保存的.m文件
>> func_a(pi)
ans =

    -1%再次尝试计算，发现已经载入成功
%isa(var,'function_handle')演示
>> isa(func_a,'function_handle')
ans =

logical

   1
%isequal(funhandlea,funhandleb)演示
>> func_b=@sin;%定义函数句柄b
>> isequal(func_a,func_b)%func_a与func_b不对应同一个函数，返回0

ans =

  logical

   0

>> isequal(func_a,@cos)%func_a与@cos对应同一个函数，返回1

ans =

  logical

   1

>> isequal(func_a,cos)%这里我们没有在cos前加入@寻址，所以这里的cos不是一个句柄，报错
错误使用 cos
输入参数的数目不足。
```

那么，到这里我们Matlab新手教程(2)就结束了，我们到目前为止已经学习了Matlab中数据类型中的3种，**数值类型、字符和字符串、函数句柄**，在下一章种，我们将学习第四种：元胞数组。
