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
|6|314|Binary Tree Vertical Order Traversal|[Link](https://leetcode.com/problems/binary-tree-vertical-order-traversal/description/)|一个二叉树，返回垂直检索序列。返回的是一个链表，链表每个元素是同一列的元素，并且按照从上到下排列。|前序遍历二叉树，给每个node分配（row, column）表示其位置，并且按照column位key放入一个dictionary中。然后按照key从小到大输出元素，每个元素均为处于同一column的数字链表。（递归）||
|7|339|Nested List Weight Sum|[Link](https://leetcode.com/problems/nested-list-weight-sum/description/)|一个新定义的类 NestedInteger，包含一些API。一个NestedInteger可能只包含一个整数，也可能是一个包含整数的链表。求每个整数与其在链表中深度的乘积和。|深度优先遍历链表，对于每个元素，若为只包含一个整数的NestedInteger，则加上weighted number，否则进入调用深度优先函数，进入下一层链表。（递归）||
|8|1650|Lowest Common Ancestor of a Binary Tree III|[Link](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree-iii/description/)|一个二叉树，每个节点不仅包含值、指向左右子树的指针，还包含其指向其父母的指针。求两个节点的最小共同祖先。|假设两个节点分别为p和q，二叉树的根节点为root，p和q的最小共同祖先为target，那么路径p->root->q->target和q->root->p->target的长度是相同的。所以根据这个思路，可以从p和q向上溯源，知道访问到target节点。（注意循环中有可能已经访问到target节点了）||
|9|236|Lowest Common Ancestor of a Binary Tree|[Link](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/)|求二叉树中两个节点p和q的最低共同祖先节点。|最小公共子节点拥有一个特性：其左右子树分别包含p和q。所以，首先判断当前节点是不是p或者q中的一个，如果是，则返回当前节点。否则，判断当前节点左右子树分别包含p和q，如果是，则当前节点即为p和q最低共同祖先。||
|10|938|Range Sum of BST|[Link](https://leetcode.com/problems/range-sum-of-bst/description/)|求二叉树中节点值位于给定范围内的和。|遍历树中每个节点（深度优先，广度优先，前/后/中序遍历），判断节点值是否位于给定范围，若是，则加到最终的结果中去。||
|11|528|Random Pick with Weight|[Link](https://leetcode.com/problems/random-pick-with-weight/description/)|给定一个权重数组，数组每个值代表当前位置的权重。部署一个随机选择位置的函数，每个位置被选中的几率正比于该位置的权重。|求权重数组的累积分布函数(Cumulative Distribution Function)。然后，在1和权重和之间随机生成一个数，生成的随机数在cdf中的所处位置就是应该返回的位置。在cdf中查找随机数的时候，要用二分法查找。||
|12|71|Simplify Path|[Link](https://leetcode.com/problems/simplify-path/description/)|简化表示unix路径的字符串。|用'/'将字符串分割为list，遍历这个list，如果元素是'.'或''，直接删除，如果是'..'，则删除当前元素和上一个元素（注意遍历下标的变化）。最后用'/'将list中的字符串连接起来，返回。||
|13|1091|Shortest Path in Binary Matrix|[Link](https://leetcode.com/problems/shortest-path-in-binary-matrix/description/)|给定一个grid，由0和1组成，求从grid左上角到右下角最短路径。要求路径上的元素均为0。|运用队列，广度优先遍历grid中的0元素点，每一层路径节点数加1，直到访问到右下角节点，返回路径长度。||
|13|1091|Shortest Path in Binary Matrix|[Link](https://leetcode.com/problems/shortest-path-in-binary-matrix/description/)|给定一个grid，由0和1组成，求从grid左上角到右下角最短路径。要求路径上的元素均为0。|运用队列，广度优先遍历grid中的0元素点，每一层路径节点数加1，直到访问到右下角节点，返回路径长度。||
|14|199|Binary Tree Right Side View|[Link](https://leetcode.com/problems/binary-tree-right-side-view/description/)|求一个二叉树从其右方看到的数从上到下组成的数组。|递归法：分别求左右子树的从右方看到的数组，然后比较其结果，生成最终结果（右子树结果会遮挡左子树结果）。或者广度优先遍历树，每一层最后一个元素即为该层从右方看到的结果。||
|15|1570|Dot Product of Two Sparse Vectors|[Link](https://leetcode.com/problems/dot-product-of-two-sparse-vectors/description/)|存储稀疏矩阵，并且创造求稀疏矩阵内积的函数。|用directionary存储稀疏矩阵，key是位置，value是数值。求内积的时候，相同key的value乘积。注意遍历长度较小的directionary。||
|16|88|Merge Sorted Array|[Link](https://leetcode.com/problems/merge-sorted-array/description/)|合并两个有序数组，结果存储到其中一个数组中。|从右向左依次比较两个数组的元素，大的那个被选中，存入合并后的数组中，并更新对应指针。注意其中一个数组可能向遍历完。||
|17|50|Pow(x, n)|[Link](https://leetcode.com/problems/powx-n/description/)|利用普通运算符实现Pow(x, n)函数。|联想n的二进制形式，Pow(x, n)即是由x的一系列幂的乘积。如Pow(x, 10)，10 = b1010，则Pow(x, 10) = x^8 * x ^2。所以可以对n进行位运算，每次向右移动一位，x更新为对应的幂，当n二进制末尾为1的时候，结果乘以x的值。直到n位0为止。||
|18|162|Find Peak Element|[Link](https://leetcode.com/problems/find-peak-element/description/)|找到数组中的一个峰，峰定义为数组元素比前后元素都大。同时规定，数组边界外为无限小。|二分查找。左右指针，分别从左往右、从右往左，向中间查找。每次查找中间元素，若该元素比临近元素大，则返回该元素位置。否则则有两种情况：（1）该中间元素不大于其右边元素，则待查找元素必位于右半部分；（2）该中间元素大于其右边元素（即不大于其左边元素），则待查找元素必位于左半部分。注意循环条件：left < right - 1。这样可以使得mid元素始终有邻近元素，同时可以处理数组长度小于3的情况。最后返回时要返回left和right中对以应元素大的那个。||
|19|543|Diameter of Binary Tree|[Link](https://leetcode.com/problems/diameter-of-binary-tree/description/)|二叉树的直径为树中距离最远的连个节点之间的距离，注意这两个节点不一定要穿过根节点。。|定义一个计算每个节点深度的函数，该函数递归式地计算节点左右子树的深度，该节点深度则为左右子树深度较大值加1。在这个过程中，评估穿过每个节点的最长路径，即左右子树深度之和。遍历所有节点之后，即可得到最长路径的长度，即diameter。||
|20|146|LRU Cache|[Link](https://leetcode.com/problems/lru-cache/description/)|设计一个数据结构，遵循Least Recently Used (LRU) cache的规则。|(1) 利用collections.OrderedDict模块，保持插入键值的顺序。访问某个键时，获得对应的值后将该键移除后重新插入，使得它位于字典头部。插入键值时，如果存储空间满了，则需先移除字典尾部元素，再插入新键值。（2）如果不允许使用该模块，则可以利用双向链表实现，保存链表首尾，方便插入、删除。同时维持一个字典，可以快速访问键值。||
|21|1|Two Sum|[Link](https://leetcode.com/problems/two-sum/description/)|给定一个数组，找到两个元素，其和为固定值target。|(1) 先把数组排序，然后利用双指针来寻找两个元素。（2）创建hashmap，键为元素值，值为元素位置。遍历数组，利用target和元素值来查询是否哈希表中已经有对应元素了。||
|22|125|Valid Palindrome|[Link](https://leetcode.com/problems/valid-palindrome/description/)|判断一个字符串中的英文字符组成的字符串是否是会问字符。|首位指针，对于非英文字符，跳过。英文字符则比较首位指针对应字符是否一致，不一致则不是回文字符串。注意一些字符串操作函数：lower，isalnum等。||
|23|791|Custom Sort String|[Link](https://leetcode.com/problems/custom-sort-string/description/)|给定一个字符串，和一个字符串order，按照order中字符顺序来排列字符串。|（1）按照order中字符，设定26个英文字母的顺序，按照这个顺序利用sort函数来排列字符串。（2）创建一个hashmap，统计字符串中每个字符的频率。然后遍历order字符串，如果字符在hashmap中，则按照频率扩展字符串。最后，再把没有在order中出现的字符附加上去。||
|24|921|Minimum Add to Make Parentheses Valid|[Link](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/description/)|给定一个由左右括号组成的字符串，问最少添加多少额外的括号，使得该字符串是正确的括号组合。|两个变量left和right分别记录左右括号数量，遍历字符串，若为左括号，则left加1，若为右括号，若left大于0，则left减1，否则right加1。最后返回left+right。||
|25|973|K Closest Points to Origin|[Link](https://leetcode.com/problems/k-closest-points-to-origin/description/)|给定一系列二维点，返回k个离原点最近的点。|k最小值问题。可以用栈来解决，也可用快速选择来解决。用栈，可以用heapq模块，注意栈是最小栈，而且heapq支持元素为tuple或list，根据元素第一个值来构建栈。||


