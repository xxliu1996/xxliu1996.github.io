---
title: '【编程】：《剑指offer》题目思路整理'
date: 2024-04-17
permalink: /posts/2024/04/blog-coding-interview-questions-summary/
tags:
  - 剑指offer
  - 编程
  - C++
  - 算法
---
<img src='/images/blog/2024-coding-interview-questions-summary/2024-coding-interview-jianzhioffer.jpg'>

*本文主要内容，来自于本人在阅读何海淘《剑指offer》这本书过程中，对题目解题思路的整理。牢记这些题目和思路可以帮助我们应对常见的编程面试题，我认为是很有帮助的。*

|题号|题目标题|题目介绍|解题思路|详解|
|---|-------|------|-------|----|
|1|赋值运算符函数|<img src='/images/blog/2024-coding-interview-questions-summary/problem-1.jpeg'>|一个简单的办法是我们先用new分配新内容再用delete释放已有的内容。这样只在分配内容成功之后再释放原来的内容，也就是当分配内存失败时我们能确保 CMyString 的实例不会被修改。我们还有一个更好的办法是先创建一个临时实例，再交换临时实例和原来的实例。||