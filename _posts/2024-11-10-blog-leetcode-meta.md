---
title: 'Leetcode Meta面试高频题'
date: 2024-11-10
permalink: /posts/2024/11/blog-leetcode-meta/
tags:
  - Leetcode
  - Meta
  - 编程
  - Python
  - 算法
---
<img src='/images/blog/2024-coding-interview-questions-summary/2024-coding-interview-jianzhioffer.jpg'>

*本文主要内容，来自于本人在阅读何海淘《剑指offer》这本书过程中，对题目解题思路的整理。牢记这些题目和思路可以帮助我们应对常见的编程面试题，我认为是很有帮助的。*

|编号|题号|题目标题|题目链接|题目介绍|解题思路|详解|
｜---|---|-------|------|-------|-------|---|
|1|1249|Minimum Remove to Make Valid Parentheses|[Link](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/description/)|字符串中有多余的括号，去除括号，使得括号的组合是合理的。|先把字符串转换为list，然后用栈来记录左括号的位置，遍历到右括号的时候，如果栈非空，则栈顶元素出栈，否则将对应的字符变为空字符。遍历完成之后，如果栈非空，则将栈内对应位置的字符设为空字符。||