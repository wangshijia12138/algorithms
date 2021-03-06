## 级别三  【二叉树的广度优先遍历】
***

>有一棵二叉树，每个节点由一个大写字母标识(最多26个节点）。现有两组字母，分别表示后序遍历（左孩子->右孩子->父节点）
>和中序 遍历（左孩子->父节点->右孩子）的结果，请输出层次遍历的结果
>
>输入描述：
>输入为两个字符串，分别是二叉树的后续遍历和中序遍历结果。
>
>输出描述：
>输出二叉树的层次遍历结果。
>
>```
>示例1：
>输入：
>CBEFDA CBAEDF
>输出：
>ABDCEF
>```

## 级别三   【找单词】

> 给一个字符串和一个二维字符数组，如果该字符串存在于该数组中，则按字符串的字符顺序输出字符串每个字符所在单元格的位置下标字符串，如果找不到返回字符串"N"。
>
> 1.需要按照字符串的字符组成顺序搜索，且搜索到的位置必须是相邻单元格，其中“相邻单元格”是指那些水平相邻或垂直相邻的单元格。
>
> 2.同一个单元格内的字母不允许被重复使用。
>
> 3.假定在数组中最多只存在一个可能的匹配。
>
> ```
> 输入描述:
> 
> 1.第1行为一个数字（N）指示二维数组在后续输入所占的行数。
> 2.第2行到第N+1行输入为一个二维大写字符数组，每行字符用半角,分割。
> 3.第N+2行为待查找的字符串，由大写字符组成。
> 4.二维数组的大小为N*N，0<N<=100。
> 5.单词长度K，0<K<1000。
> 
> 输出描述:
> 输出一个位置下标字符串，拼接格式为：第1个字符行下标+","+第1个字符列下标+","+第2个字符行下标+","+第2个字符列下标...+","+第N个字符行下标+","+第N个字符列下标
> 
> 输入
> 4
> A,C,C,F
> C,D,E,D
> B,E,S,S
> F,E,C,A
> ACCESS
> 输出
> 0,0,0,1,0,2,1,2,2,2,2,3
> 
> 说明
> ACCESS分别对应二维数组的[0,0] [0,1] [0,2] [1,2] [2,2] [2,3]下标位置
> ```

思路:

>1.首先找到第一个匹配的元素
>
>2.基于第一个匹配的元素不断找他上下左右的元素



## 级别三   【求满足条件的最长子串的长度】

>给定一个字符串，只包含字母和数字，按要求找出字符串中的最长（连续）子串的长度，字符串本身是其最长的子串，子串要求：
>
>1、只包含1个字母(a~z, A~Z)，其余必须是数字；
>
>2、字母可以在子串中的任意位置；
>
>如果找不到满足要求的子串，如全是字母或全是数字，则返回-1。
>
>输入描述：
>
>字符串(只包含字母和数字)
>
>输出描述：
>
>子串的长度
>
>```
>示例1：
>
>输入
>abC124ACb
>
>输出
>4
>```

思路:

>双指针









## 级别三   【简易内存池】

>题目描述
>请实现一个简易内存池,根据请求命令完成内存分配和释放。
>内存池支持两种操作命令，REQUEST和RELEASE，其格式为：
>REQUEST=请求的内存大小 表示请求分配指定大小内存，如果分配成功，返回分配到的内存首地址；如果内存不足，或指定的大小为0，则输出error。
>RELEASE=释放的内存首地址 表示释放掉之前分配的内存，释放成功无需输出，如果释放不存在的首地址则输出error。
>注意：
>1.内存池总大小为100字节。
>2.内存池地址分配必须是连续内存，并优先从低地址分配。
>3.内存释放后可被再次分配，已释放的内存在空闲时不能被二次释放。
>4.不会释放已申请的内存块的中间地址。
>5.释放操作只是针对首地址所对应的单个内存块进行操作，不会影响其它内存块。
>
>解答要求
>时间限制: 1000ms, 内存限制: 256MB
>输入
>首行为整数 N , 表示操作命令的个数，取值范围：0 < N <= 100。
>接下来的N行, 每行将给出一个操作命令，操作命令和参数之间用 “=”分割。
>
>输出
>见题面输出要求
>
>```
>样例
>输入样例1
>2
>REQUEST=10
>REQUEST=20
>输出样例1
>0
>10
>输入样例2
>5
>REQUEST=10
>REQUEST=20
>RELEASE=0
>REQUEST=20
>REQUEST=10
>输出样例2
>0
>10
>30
>0
>提示
>第一条指令，申请地址0~9的10个字节内存，返回首地址0
>第二条指令，申请地址10~29的20字节内存，返回首地址10
>第三条指令，释放首地址为0的内存申请，0~9地址内存被释放，变为空闲，释放成功，无需输出
>第四条指令，申请20字节内存，09地址内存连续空间不足20字节，往后查找到3049地址，返回首地址30
>第五条指令，申请10字节，0~9地址内存空间足够，返回首地址0
>```







## 级别三   【工作时长】

小明上班打卡时间为AA:BB

## 级别三   【仿LISP运算】

>LISP 语言唯一的语法就是括号要配对。 形如(OP P1 P2 …)，括号内元素由单个空格分割。 其中第一个
>元素 OP 为操作符，后续元素均为其参数，参数个数取决于操作符类型 注意：参数 P1, P2 也有可能是另外
>一个嵌套的(OP P1 P2 …) 当前 OP 类型为 add / sub / mul / div（全小写），分别代表整数的加减乘除法
>简单起见，所有 OP 参数个数均为 2
>举例:
>输入：(mul 3 -7) 输出： -21
>输入：(add 1 2) 输出：3
>输入：(sub(mul 2 4) (div 9 3)) 输出：5
>输入：(div 1 0) 输出：error 题目涉及数字均为整数，可能为负；
>不考虑 32 位溢出翻转，计算过程中也不会发生 32 位溢出翻转 除零错误时，
>输出 “error”，除法遇除不尽，向下取整，即 3 / 2 = 1
>
>```
>输入描述：
>输入为长度不超过 512 的字符串，用例保证了无语法错误
>输出描述：
>输出计算结果或者“error”
>示例 1
>输入：(div 12 (sub 45 45))
>输出：
>error
>```



## 级别三   【高效的任务规划】

## 级别三   【计算疫情扩散时间】

>
>
>计算疫情扩散的时间
>
>计算疫情扩散时间 | 时间限制：1秒 | 内存限制：32768K | 语⾔限制：不限
>
>在⼀个地图中(地图由n*n个区域组成），有部分区域被感染病菌。感染区域每天都会把周围（上下左右）的4个区域感染。
>
>请根据给定的地图计算，多少天以后，全部区域都会被感染。
>
>如果初始地图上所有区域全部都被感染，或者没有被感染区域，返回-1
>
>收起
>
>输⼊描述:
>
>⼀⾏N*N个数字（只包含0,1，不会有其他数字）表⽰⼀个地图，数字间⽤,分割，0表⽰未感染区域，1表⽰已经感染区域
>
>每N个数字表⽰地图中⼀⾏，输⼊数据共表⽰N⾏N列的区域地图。
>
>例如输⼊1,0,1,0,0,0,1,0,1，表⽰地图
>
>1
>
>,
>
>0
>
>,
>
>1
>
>0
>
>,
>
>0
>
>,
>
>0
>
>1
>
>,
>
>0
>
>,
>
>1
>
>输出描述:
>
>⼀个整数，表⽰经过多少天以后，全部区域都被感染
>
>⽰例1
>
>输⼊
>
>1
>
>,
>
>0
>
>,
>
>1
>
>,
>
>0
>
>,
>
>0
>
>,
>
>0
>
>,
>
>1
>
>,
>
>0
>
>,
>
>1
>
>输出
>
>2
>
>说明
>
>1天以后，地图中仅剩余中⼼点未被感染；2天以后，全部被感染。
>
>⽰例2
>
>输⼊
>
>0
>
>,
>
>0
>
>,
>
>0
>
>,
>
>0
>
>输出
>
>\-
>
>1
>
>说明
>
>⽆感染区域
>
>⽰例3
>
>输⼊
>
>1
>
>,
>
>1
>
>,
>
>1
>
>,
>
>1
>
>,
>
>1
>
>,
>
>1
>
>,
>
>1
>
>,
>
>1
>
>,
>
>1
>
>输出
>
>\-
>
>1
>
>说明
>
>全部都感染
>
>备注:
>
>1
>
><
>
>=
>
>N
>
><
>
>2
>
>0
>
>0
>
>解法：改点是否会被感染，取决于改点的周围的四个点，是否有1 存在

## 级别三   【斗地主之顺子】

## 级别三   【最长广播效应】

## 级别三   【可以组成网络的服务器】