---
title: '【编程】：《剑指offer》题目思路整理'
date: 2024-10-26
permalink: /posts/2024/10/blog-coding-interview-questions-summary/
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
|3|二维数组中的查找|题目：在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。|首先选取数组中右上角的数字。如果该数字等于要查找的数字，查找过程结束；如果该数字大于要查找的数字，剔除这个数字所在的列；如果该数字小于要查找的数字，剔除这个数字所在的行。也就是说如果要查找的数字不在数组的右上角，则每一次都在数组的查找范围中剔除一行或者一列，这样每一步都可以缩小查找的范围，直到找到要查找的数字，或者查找范围为空。||
|4|替换空格|题目：请实现一个函数，把字符串中的每个空格替换成“%20”。例如输入“We are happy.”，则输出“We%20are%20happy.”|从后往前替换空格。||
|5|从尾到头打印链表|题目：输入一个链表的头结点，从尾到头反过来打印出每个结点的值。|运用栈或者递归实现。||
|6|重建二叉树|题目：输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建出图2.6所示的二叉树并输出它的头结点。|前序遍历第一个是根结点，对应在中序遍历中则把左右子树分开。利用这一点，不断找根节点和左右子树。||
|7|用两个栈实现队列|题目：用两个栈实现一个队列。队列的声明如下，请实现它的两个函数appendTail和deleteHead，分别完成在队列尾部插入结点和在队列头部删除结点的功能。|两个栈分别用于入队和出队。Stack1用于入队，每次在队列尾部插入元素，就插入Stack1栈顶；Stack2用于出队，出队时若Stack1为空，则直接弹出Stack2栈顶元素，否则则把Stack1中元素逐个按顺序压入Stack2中，再弹出Stack2栈顶元素。||
|8|旋转数组的最小数字|题目：把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。|二分法查找，对比中间元素和首尾元素的大小来缩小搜索范围，直至找到最小值。对于特殊情况：首尾元素和中间元素大小相等，则只好用顺序查找的方式了。||
|9|斐波那契数列|题目：写一个函数，输入n，求斐波那契（Fibonacci）数列的第n项。|避免递归解法。一步步地计算得到第n项。||
|10|二进制中1的个数|题目：请实现一个函数，输入一个整数，输出该数二进制表示中 1 的个数。例如把9表示成二进制是1001，有2位是1。因此如果输入9，该函数输出2。|输入数字不变，用一个unsigned int整数flag与输入数字做与运算，flag初始值为1，不断左移一位，便可从右至左统计输入数字中1的个数。||
|11|数值的整数次方|题目：实现函数 double Power（double base, int exponent），求 base 的exponent次方。不得使用库函数，同时不需要考虑大数问题。|通过不断累乘实现。注意处理底数为0以及指数为0和负数的情况。||
|12|打印1到最大的n位数|题目：输入数字n，按顺序打印出从1最大的n位十进制数。比如输入3，则打印出1、2、3一直到最大的3位数即999。|为了应对大数情况，应该用数组或者字符串来储存数字。运用递归可以更好地解决这个问题。||
|13|在O(1)时间删除链表节点|题目：给定单向链表的头指针和一个结点指针，定义一个函数在 O（1）时间删除该结点。|把带删除节点的下一个节点的值复制到待删除节点，然后删除下一个节点（间接删除了目标节点）。注意考虑特殊情况：删除尾节点，以及链表中只有一个节点。||
|14|调整数组顺序使奇数位于偶数前面|题目：输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。|双指针，一个指针从左往右移动，一个指针从右往左移动，当左指针指向偶数而右指针指向奇数时，交换这两个数。||
|15|链表中倒数第k个结点|题目：输入一个链表，输出该链表中倒数第 k 个结点。为了符合大多数人的习惯，本题从1 开始计数，即链表的尾结点是倒数第1 个结点。例如一个链表有6个结点，从头结点开始它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个结点是值为4的结点。|双指针。一个指针先从头指针走k步，另一个指针也从头指针开始便利链表，二者之间始终保持k步的距离，当第一个指针指向空指针的是时候，第二个指针正好指向倒数第k个指针。注意考虑链表为空，k = 0，以及k大于链表节点数的情况。||

注解
* 左移运算符m<<n表示把m左移n位。左移n位的时候，最左边的n位将被丢弃，同时在最右边补上n个0。右移运算符m>>n表示把m右移n位。右移n位的时候，最右边的n位将被丢弃。但右移时处理最左边位的情形要稍微复杂一点。如果数字是一个无符号数值，则用0填补最左边的n位。如果数字是一个有符号数值，则用数字的符号位填补最左边的n位。也就是说如果数字原先是一个正数，则右移之后在最左边补n个0；如果数字原先是负数，则右移之后在最左边补n个1。
* 除法的效率比移位运算要低得多，在实际编程中应尽可能地用移位运算符代替乘除法。
* 一个整数减去 1 之后再和原来的整数做位与运算，得到的结果相当于是把整数的二进制表示中的最右边一个1变成0。很多二进制的问题都可以用这个思路解决。
* 我们用右移运算符代替了除以2，用位与运算符代替了求余运算符（%）来判断一个数是奇数还是偶数。位运算的效率比乘除法及求余运算的效率要高很多。既然要优化代码，我们就把优化做到极致。




