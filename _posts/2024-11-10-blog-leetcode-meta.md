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
<img src='/images/blog/2024-leetcode-meta/blog-leetcode-meta-1.png'>

*2024年9月份开始找全职的时候，接到了Meta的面试。面试包含很多coding环节，一般是要求在45min内解决两道coding问题。所以在这里总结Meta高频题（Top 100）的解题思路。*

|编号|题号|题目标题|题目链接|题目介绍|解题思路|详解|
|---|----|-------|------|-------|-------|---|
|1|1249|Minimum Remove to Make Valid Parentheses|[Link](https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/description/)|字符串中有多余的括号，去除括号，使得括号的组合是合理的。|先把字符串转换为list，然后用栈来记录左括号的位置，遍历到右括号的时候，如果栈非空，则栈顶元素出栈，否则将对应的字符变为空字符。遍历完成之后，如果栈非空，则将栈内对应位置的字符设为空字符。||
|2|408|Valid Word Abbreviation|[Link](https://leetcode.com/problems/valid-word-abbreviation/description/)|省略一部分字符，用字符个数代替，数字不能以0开头，同时两段省略字符串不能相连。|双指针。同步遍历原字符串和缩写字符串，如果是字母，比较是否相同，如果缩写字符串是数字，则将原字符串指针向后移动相应位置。当一个指针到达字符串末尾时，另一个指针也要到达末尾，否则就不是合规缩写。||
|3|227|Basic Calculator II|[Link](https://leetcode.com/problems/basic-calculator-ii/description/)|计算一个表示加减乘除运算的字符串的运算结果，字符串只包含加减乘除、数字和空格。|遍历字符串时，用pre_op储存上一个操作符。遇到数字，累加得到操作数字；遇到空格，跳过；遇到运算符，则查看pre_op，如果是加减号，则把当前操作数按正负存入栈中，若是乘除号，则栈顶元素出栈，和当前操作数运算后再入栈。最后返回栈中所有数字的和。||
|4|680|Valid Palindrome II|[Link](https://leetcode.com/problems/valid-palindrome-ii/description/)|给定一个字符串，在允许至多删除一个字符的情况下，是否可以得到一个回文字符串（Palindrome）。|双指针，一个左至右，一个从右至左。向中间靠拢，判断所指字符是否相同。如果遇到字符不同的情况，则分别判断去除左指针字符和去除右指针字符后，是否是一个回文字符串。需要一个标志符，来显示是否已经去掉字符了。（递归）||
|<span style="color:red">5</span>|215|Kth Largest Element in an Array|[Link](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)|找到数组中第k大的数。|快速选择，基于快速排序。选定pivot，把数组划分为比pivot小，和pivot相等，比pivot大的部分，通过三个数组的长度，来判断第k大数组位于那个子数组，再对其进行快速排序。运用heap，构造一个包含k个元素的heap，heap顶部元素为heap里面的最小值。||
