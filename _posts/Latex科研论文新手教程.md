---
title: LaTeX科研论文新手教程
date: 2022-10-18 17:23:09
tags:
- LaTeX
- 科研论文
categories:
- LaTeX
mathjax: true
---

# LaTeX科研论文新手教程（1）

​	LaTeX是当今世界最流行和使用最广泛的TeX宏集。LaTeX在Plain TeX的基础上增加了很多新的功能，使用者可以更加方便地运用TeX的强大功能完成一些文档编辑任务。使用LaTeX的优势在于，用户不需要自己设计命令和宏等，即使用户没有排版和程序设计的背景知识，也可以熟练应用TeX提供的强大功能。因此，即使用户并不是很了解TeX，也可以在几天甚至几小时内生成很多具有书籍质量的印刷品。对于**科研论文**来说，当中会应用许多复杂的表格和数学公式。LaTeX的表现就更为出色，因此它非常适用于生成高质量印刷品的科技和数学类文档。

<!-- more -->

​	在笔者看来，目前比较好用的LaTeX写作软件有3个，分别是[overleaf](https://cn.overleaf.com/)，[CTeX](http://www.ctex.org/HomePage)，以及[MiKTeX](https://miktex.org/)，其中overleaf是一个云端的写作平台，许多期刊的格式可以直接导入，甚至投稿也可以通过overleaf完成。而CTeX是中国运筹协会发布的一款TeX的中文套装，其中是把MiKTeX和一些常用的相关工具，例如GSview、WinEdt等包装在一起制作的一个简易安装程序，所以有的时候它总会面临一些侵权问题。那么MiKTeX就是Windows平台下最好的TeX平台了。

## LaTeX基本框架

一篇LaTeX文档的基本框架应该如下所示：

```latex
\documentclass{article}
\begin{document}
\title{...}
\author{...}
\institute{...}
\maketitle
\begin{abstract}
.
.
.
\end{abstract}
\keywords{...;...;...}
\section{...}
\subsection{...}
\subsection{...}
\section*{Acknowledgements}
\begin{thebibliorgraphy}
\bibitem{}
\bibitem{}
.
.
.
\end{thebibliorgraphy}
\end{document}
```

​	接下来我们我们将分别讨论：

### （1）\documentclass{类}

​	这是你一篇文章的奠基处，在这条语句中你需要确定整篇文章的处理格式，在期刊或者会议论文一般可选为*article*，再附上控制全局格式的选项，比如字体、字号、页面格式、纸张大小等。现在有很多的期刊都直接提供类模板，比如*Lecture Notes in Computer Science*提供的模板为lncs.cls，你只需要把相应的类名lncs放到{类}里就可以了。

**注意**：.cls文件需要放在当前文件夹下，否则会因为找不到该文件而提示出错。

### （2）\usepackage{宏包}

​	宏包是用来增强功能的，你可以理解为你在游戏中增加进去的MOD，它能让你拥有更好的体验，宏包包含在.sty文件中，主要应用的宏包如下：

1. CJK支持中文环境，对应宏包命令为*\usepackage{CJK}*，如果想在LaTeX中使用中文，需要使用这个宏包。

2. 我们在写论文时，英文字体通常使用***Times New Roman***，这就需要用到宏包命令*\usepackage{times}*。

3. 论文中不可避免的需要插入图片，需要用到的宏包是*\usepackage{graphicx}*。

4. 在pdftex文件中生成的pdf是不具有超链接功能的，但如果需要也是需要添加宏包的，宏包命令为*\usepackage{pyperref}*。

以上为导言区，完成了导言部分，接下来就到了正文部分，正文部分位于

```latex
\begin{document}
.
.
.
\end{document}
```

之间。LaTeX命令的作用对象和范围类似于HTML的标签，有开始和结束标志，开始位置内会定义一些表现格式。导言区还可能有\pagestyle{选项}，页面样式，比如empty选项表示没有页眉和页脚。除此之外导言区还有其他全局性的设置。

### （3）\title{标题}

​	正文部分首先是文章标题。题目
