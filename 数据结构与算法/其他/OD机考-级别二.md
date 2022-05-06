### 1.【太阳能板最大面积】

>给航天器一侧加装长方形和正方形的太阳能板(图中的斜线区域)
>需要先安装两个支柱(图中的黑色竖条)
>再在支柱的中间部分固定太阳能板
>但航天器不同位置的支柱长度不同
>太阳能板的安装面积受限于最短一侧的那支支柱的长度
>
>现提供一组整型数组的支柱高度数据
>假设每个支柱间的距离相等为一个单位长度
>计算如何选择两根支柱可以使太阳能板的面积最大
>
>```
>   输入描述
>    10,9,8,7,6,5,4,3,2,1
>    注释，支柱至少有两根，最多10000根，能支持的高度范围1~10^9的整数
>
>    柱子的高度是无序的
>    例子中的递减是巧合
>
>    输出描述
>    可以支持的最大太阳板面积:(10m高支柱和5m高支柱之间)
>    25
>
>    示例1
>    输入
>    10,9,8,7,6,5,4,3,2,1
>    输出
>    25
>    备注 10米高支柱和5米高支柱之间宽度为5，高度取小的支柱高度也是5
>    面积为25
>    任取其他两根支柱所能获得的面积都小于25 所以最大面积为25
>```

思路:

>穷举 ,计算所有组合,取最大值

```java
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str;
        while ((str = br.readLine()) != null) {
            String[] split = str.split(",");
            int[] ints = new int[split.length];
            for (int i = 0; i < split.length; i++) {
                ints[i] = Integer.parseInt(split[i]);
            }
            solution(ints);
        }
    }

    private static void solution(int[] height) {
        int max = 0;
        for (int i = 0; i < height.length; i++) {
            for (int j = i + 1; j < height.length; j++) {
                int minHeight = Math.min(height[i], height[j]);
                max = Math.max(max, minHeight * (j - i));
            }
        }
        System.out.println(max);
    }
```



### 2.【VLAN资源池】

>Vlan是一种为局域网设备进行逻辑划分的技术
>为了标识不同的vlan 引入了vlan id 1~4094之间的整数
>定义一个vlan id 的资源池
>资源池中连续的vlan用开始vlan-结束vlan表示，
>不连续的用单个整数表示
>所有的vlan用英文逗号连接起来
>现有一个vlan资源池，业务需要从资源池中申请一个vlan
>需要你输出从vlan资源池中移除申请的vlan后的资源池
>
>输入描述
>第一行为字符串格式的vlan资源池
>第二行为业务要申请的vlan vlan的取值范围1~4094
>
>输出描述
>从输入vlan资源池中移除申请的vlan后
>字符串格式的vlan资源池
>输出要求满足题目中要求的格式，
>并且要求从小到大升序输出
>如果申请的vlan不在原资源池，输出升序排序的原资源池的字符串即可
>
>```
>示例一
>输入
>1-5
>2
>输出
>1,3-5
>说明：原vlan资源池中有1 2 3 4 5 移除2后
>剩下的1 3 4 5按照升序排列的方式为 1 3-5
>
>示例二
>输入
>20-21,15,18,30,5-10
>15
>输出
>5-10,18,20-21,30
>说明：
>原vlan资源池中有5 6 7 8 9 10 15 18 20 21 30
>移除15后 剩下的为 5 6 7 8 9 10 18 20 21 30
>按照题目描述格式并升序后的结果为5-10,18,20-21,30
>
>示例三
>输入
>5,1-3
>10
>输出
>1-3,5
>资源池中有1 2 3 5
>申请的资源不在资源池中
>将原池升序输出为1-3,5
>
>输入池中vlan数量范围为2~2094的整数
>资源池中vlan不重复且合法1~2094的整数
>输入是乱序的
>```

思路:

> step1:获取入参 处理为一个 treeSet集合,实现排序去重
> step2:去除申请参数  
>step3:按要求拼接set ,连续数字以-拼接

```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String str;
    while ((str = br.readLine()) != null) {
        // 获取入参 处理为一个 treeSet集合,实现排序去重
        String[] split = str.split(",");
        TreeSet<Integer> set = new TreeSet<>();
        for (String s : split) {
            if (s.contains("-")) {
                String[] split1 = s.split("-");
                int start = Integer.parseInt(split1[0]);
                int end = Integer.parseInt(split1[1]);
                for (int i = start; i <= end; i++) {
                    set.add(i);
                }
            } else {
                set.add(Integer.parseInt(s));
            }
        }
        // 去除申请参数
        set.remove(Integer.parseInt(br.readLine()));

        // 按要求拼接set ,连续数字以-拼接
        List<Integer> list = new ArrayList<>(set);
        int start = list.get(0);
        int end = start;
        StringBuilder sb = new StringBuilder();
        for (int i = 1; i < list.size(); i++) {
            Integer cur = list.get(i);
            if (cur == end + 1) {
                end = cur;
            } else {
                if (start== end) {
                    sb.append(end).append(",");
                } else {
                    sb.append(start).append("-").append(end).append(",");
                }
                start = end = cur;
            }
        }
        if (start== end) {
            sb.append(end).append(",");
        } else {
            sb.append(start).append("-").append(end).append(",");
        }
        System.out.println(sb.deleteCharAt(sb.length()-1));
    }
}
```

### 3.【找终点】

>一个正整数数组 设为nums
>最大为100个成员
>求从第一个成员开始正好走到数组最后一个成员所使用的最小步骤数
>3 5 9 4 2 6 8 3 5 4 3 9
>要求：
>第一步 必须从第一元素起 且 1<=第一步步长<len/2 (len为数组长度)
>
>从第二步开始只能以所在成员的数字走相应的步数，不能多不能少，
>如果目标不可达返回-1 只输出最小的步骤数量 只能向数组的尾部走不能向回走
>
>输入描述：
>有正整数数组 空格分割
>数组长度<100
>
>输出描述 ：
>正整数 最小步数
>不存在输出-1
>
>```
>例子：
>输入
>7 5 9 4 2 6 8 3 5 4 3 9
>输出
>2
>第一个可选步长选择2
>从第一个成员7开始走两步到9
>第二步：从9经过9个成员到最后
>
>例子：
>输入
>1 2 3 7 1 5 9 3 2 1
>输出
>-1
>```

思路:

>穷举所有可能  找到最小值 

```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String str;
    while ((str = br.readLine()) != null) {
        String[] split = str.split(" ");
        int[] ints = new int[split.length];
        for (int i = 0; i < split.length; i++) {
            ints[i] = Integer.parseInt(split[i]);
        }
        solution(ints);
    }
}

private static void solution(int[] members) {
    if (members.length <= 2) {
        System.out.println(1);
        return;
    }
    int min = Integer.MAX_VALUE;
    for (int i = 1; i < members.length / 2; i++) {
        min = Math.min(f(i, 1, members), min);
    }
    if (min == Integer.MAX_VALUE) {
        System.out.println(-1);
    } else {
        System.out.println(min);
    }
}

private static int f(int cur, int step, int[] members) {
    if (cur + members[cur] > members.length - 1) {
        return Integer.MAX_VALUE;
    }

    if (cur + members[cur] == members.length - 1) {
        return step + 1;
    }
    cur += members[cur];
    step++;
    return f(cur, step, members);
}
```



### 4.【喊7的次数重排】

>喊7 是一个传统的聚会游戏
>N个人围成一圈
>按顺时针从1-7编号
>编号为1的人从1开始喊数
>下一个人喊得数字是上一个人喊得数字+1
>但是当将要喊出数字7的倍数或者含有7的话
>不能喊出 而是要喊过
>
>假定N个人都没有失误。
>当喊道数字k时
>可以统计每个人喊 “过"的次数
>
>现给定一个长度n的数组
>存储打乱的每个人喊”过"的次数
>请把它还原成正确顺序
>
>即数组的第i个元素存储编号i的人喊“过“的次数
>
>输入为1行
>空格分割的喊过的次数
>注意k并不提供
>
>k不超过200
>数字个数为n
>输出描述
>
>输出为1行
>顺序正确的喊过的次数 空格分割
>
>```
>例子
>输入
>0 1 0
>输出
>1 0 0
>
>只有一次过
>发生在7
>按顺序编号1的人遇到7  所以100
>结束时的k不一定是7 也可以是 8 9
>喊过都是100
>
>例子
>输入
>0 0 0 2 1
>输出
>0 2 0 1 0
>一共三次喊过
>发生在7 14 17
>编号为2 的遇到7 17
>编号为4 的遇到14
>```
>
>

思路:

>1.获取七的总数
>
>2.模拟数七过程,重新分配这些七

```java
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str;
        while ((str = br.readLine()) != null) {
            String[] s = str.split(" ");
            int n = s.length;
            int sum = 0;
            for (int i = 0; i < n; i++) {
                sum = sum + Integer.parseInt(s[i]);
            }
            if (sum == 0) {
                System.out.println(str);
            }

            int count = 0;
            int k = 0;
            int[] res = new int[n];
            while (count < sum) {
                k++;
                if (k % 7 == 0 || String.valueOf(k).contains("7")) {
                    res[k % n] += 1;
                    count++;
                }
            }
            for (int i = 1; i < res.length; i++) {
                System.out.print(res[i] + " ");
            }
            System.out.print(res[0] + " ");
        }
    }
```



### 5. 【流水线】

>一个工厂有m条流水线
>来并行完成n个独立的作业
>该工厂设置了一个调度系统
>在安排作业时，总是优先执行处理时间最短的作业
>现给定流水线个数m
>需要完成的作业数n
>每个作业的处理时间分别为 t1,t2…tn
>请你编程计算处理完所有作业的耗时为多少
>当n>m时 首先处理时间短的m个作业进入流水线
>其他的等待
>当某个作业完成时，
>依次从剩余作业中取处理时间最短的
>进入处理
>
>```
>输入描述：
>第一行为两个整数(采取空格分隔)
>分别表示流水线个数m和作业数n
>第二行输入n个整数(采取空格分隔)
>表示每个作业的处理时长 t1,t2…tn
>0<m,n<100
>0<t1,t2…tn<100
>
>输出描述
>输出处理完所有作业的总时长
>输入
>3 5
>8 4 3 2 10
>输出
>13
>说明
>先安排时间为2,3,4的三个作业
>第一条流水线先完成作业
>调度剩余时间最短的作业8
>第二条流水线完成作业
>调度剩余时间最短的作业10
>总共耗时 就是二条流水线完成作业时间13(3+10)
>
>3 9
>1 1 1 2 3 4 6 7 8
>```

思路:

>动态规划思想,构建总耗时dp函数

```java
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str;
        while ((str = br.readLine()) != null) {
            String[] s = str.split(" ");
            int m = Integer.parseInt(s[0]);
            int n = Integer.parseInt(s[1]);
            int[] jobs = new int[n];
            String[] strs = br.readLine().split(" ");
            for (int i = 0; i < strs.length; i++) {
                jobs[i] = Integer.parseInt(strs[i]);
            }
            solution(m, jobs);
        }
    }

    /**
     * @param m    流水线条数
     * @param jobs 任务数
     */
    private static void solution(int m, int[] jobs) {
        Arrays.sort(jobs);
        // 流水线数大于任务总数时,总耗时是最后一个任务完成的时间
        if (m >= jobs.length) {
            System.out.println(jobs[jobs.length - 1]);
            return;
        }

        // 构建总耗时函数
        int[] dp = new int[m];
        for (int i = 0; i < jobs.length; i++) {
            if (i < m) {
                // 流水线之内每多一个任务都是当前最长耗时
                dp[i] = jobs[i];
            } else {
                Arrays.sort(dp);
                // 流水线之外每多一个任务都是当前最短耗时+任务耗时
                dp[i % m] = dp[0] + jobs[i];
            }
        }
        Arrays.sort(dp);
        System.out.println(dp[dp.length - 1]);
    }
```



### 6. 【最大括号深度】

>【最大括号深度】现有一字符串仅由( , ) , { , } , [ , ]六种括号组成。若字符串满足以下条件之一，则为无效字符串：
>1、任一类型的左右括号数量不相等；
>2、存在未按正确顺序（先左后右）闭合的括号。
>
>输出括号的最大嵌套深度，若字符串无效则输出0.
>0<=字符串长度<=100000
>
>输入描述：
>一个只包( , ) , { , } , [ , ]的字符串。
>
>输出描述:
>一个整数，最大括号深度
>
>示例1：
>输入:[]
>输出:1

思路:

>构建一个栈结构,模拟实现括号的匹配

```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String str;
    while ((str = br.readLine()) != null) {
        solution(str);
    }
}

private static void solution(String str) {
    if (str == null || str.length() == 0) {
        System.out.println(0);
        return;
    }
    int maxDepth = 0;
    int count = 0;
    Stack<Character> stack = new Stack<>();
    for (int i = 0; i < str.length(); i++) {
        char ch = str.charAt(i);
        if ('(' == ch) {
            stack.push(')');
            count = 0;
        } else if ('[' == ch) {
            stack.push(']');
            count = 0;
        } else if ('{' == ch) {
            stack.push('}');
            count = 0;
        } else {
            if (stack.peek() != ch) {
                System.out.println(0);
                return;
            } else {
                stack.pop();
                count++;
                maxDepth = Math.max(maxDepth, count);
            }
        }
    }
    System.out.println(maxDepth);
}
```



### 7. 【字符串序列判定】

>字符串序列判定
>
>输⼊两个字符串S和L，都只包含英⽂⼩写字母。S长度<=100,L长度<=500000。判定S是否是L的有效字串。
>
>判定规则：
>
>S中的每个字符在L中都能找到（可以不连续），且S在L中字符的前后顺序与S中顺序要保持⼀致。
>
>例如：S=’ace’是L='abcde’的⼀个⼦序列且有效字符是a,c,e,⽽aec不是有效⼦序列，且有效字符只有ae
>
>输⼊描述：
>
>输⼊两个字符串S和L，都只包含英⽂⼩写字母。S长度<=100,L长度<=500000。先输⼊S,再输⼊L，每个字符串占⼀⾏。
>
>输出描述：
>
>S串最后⼀个有效字符在L中的位置（⾸位从0开始计算，⽆有效字符返回-1）
>
>⽰例：
>
>输⼊ 
>
>ace
>
>abcdqwe
>
>输出 4

思路:

>双指针,两个字符串各一个,一旦子字符串的指针可以到最后,则证明该字符串是子串

```java
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str;
        while ((str = br.readLine()) != null) {
            solution(str, br.readLine());
        }
    }

    private static void solution(String s, String t) {
        int fir = 0;
        int sec = 0;

        while (fir < s.length() || sec < t.length()) {
            if (s.charAt(fir) == t.charAt(sec)) {
                fir++;
            }
            sec++;
        }
        if (fir == s.length()) {
            System.out.println(sec - 1);
        } else {
            System.out.println(-1);
        }
    }
```



### 8.【数组组成的最小数字】

>给定一个整型数组，请从该数组中选择3个元素组成最小数字并输出（如果数组长度小于3，则选择数组中所有元素来组成最小数字）。
>
>```
>输入描述:
>一行用半角逗号分割的字符串记录的整型数组，0 < 数组长度 <= 100，0 < 整数的取值范围 <= 10000。
>输出描述:
>由3个元素组成的最小数字，如果数组长度小于3，则选择数组中所有元素来组成最小数字。
>输入
>21,30,62,5,31
>输出
>21305
>
>数组长度超过3，需要选3个元素组成最小数字，21305由21,30,5三个元素组成的数字，为所有组合中最小的数字
>```

思路：

>1.筛选出数组中最小的三个数 2.通过特定的排序逻辑进行排序

```java
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str;
        while ((str = br.readLine()) != null) {
            solution(str.split(","));
        }
    }

    private static void solution(String[] strs) {
        String[] newStr = null;
        if (strs.length > 3) {
            Arrays.sort(strs, new Comparator<String>() {
                @Override
                public int compare(String o1, String o2) {
                    return (Integer.parseInt(o1) - Integer.parseInt(o2));
                }
            });
            newStr = Arrays.copyOf(strs, 3);
        } else {
            newStr = strs;
        }
        Arrays.sort(newStr, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return (o1 + o2).compareTo(o2 + o1);
            }
        });
        StringBuilder sb = new StringBuilder();
        for (String s : newStr) {
            sb.append(s);
        }
        System.out.println(sb);
    }
```

### 9. 【最长的字符串长度(一)】

>











### 10. 【找朋友】

>在学校中，N个⼩朋友站成⼀队， 第i个⼩朋友的身⾼为height[i]， 第i个⼩朋友可以看到的第⼀个⽐⾃⼰身⾼更⾼的⼩朋友j，那么j是i的好朋友(要求j > i)。
>请重新⽣成⼀个列表，对应位置的输出是每个⼩朋友的好朋友位置，如果没有看到好朋友，请在该位置⽤0代替。
>⼩朋友⼈数范围是 [0, 40000]。
>
>输⼊描述：
>第⼀⾏输⼊N，N表示有N个⼩朋友 第⼆⾏输⼊N个⼩朋友的身⾼height[i]，都是整数
>
>输出描述：
>输出N个⼩朋友的好朋友的位置
>
>```
>示例1：
>输入
>2
>100 95
>
>输出
>0 0
>```

思路:

>穷举法

```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String str;
    while ((str = br.readLine()) != null) {
        int N = Integer.parseInt(str);
        int[] heights = new int[N];
        String[] s = br.readLine().split(" ");
        for (int i = 0; i < s.length; i++) {
            heights[i] = Integer.parseInt(s[i]);
        }
        solution(heights);
    }
}

private static void solution(int[] heights) {
    int[] friends = new int[heights.length];
    for (int i = 0; i < heights.length; i++) {
        boolean flag = false;
        for (int j = i + 1; j < heights.length; j++) {
            if (heights[j] > heights[i]) {
                flag = true;
                friends[i] = j;
                break;
            }
        }
        if (!flag) {
            friends[i] = 0;
        }
    }
    for (int friend : friends) {
        System.out.print(friend + " ");
    }
}
```



### 11.【一种字符串压缩表示的解压】

>有一种简易压缩算法：针对全部为小写英文字母组成的字符串，
>将其中连续超过两个相同字母的部分压缩为连续个数加该字母
>其他部分保持原样不变.
>例如字符串aaabbccccd 经过压缩变成字符串 3abb4cd
>请您编写解压函数,根据输入的字符串,
>判断其是否为合法压缩过的字符串
>若输入合法则输出解压缩后的字符串
>否则输出字符串"!error"来报告错误
>
>输入描述
>输入一行，为一个ASCII字符串
>长度不超过100字符
>用例保证输出的字符串长度也不会超过100字符串
>
>输出描述
>若判断输入为合法的经过压缩后的字符串
>则输出压缩前的字符串
>若输入不合法 则输出字符串"!error"
>```
>示例一：
>输入
>4dff
>输出
>ddddff
>说明
>4d扩展为4个d ，故解压后的字符串为ddddff
>
>示例二
>输入
>2dff
>输出
>!error
>说明
>2个d不需要压缩 故输入不合法
>
>示例三
>输入
>4d@A
>输出
>!error
>说明
>全部由小写英文字母做成的字符串，压缩后不会出现特殊字符@和大写字母A
>故输入不合法
>
>```

思路：

>遍历到数字时统计次数,遍历到字母时基于次数恢复压缩前字符序列

```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String str;
    while ((str = br.readLine()) != null) {
        solution(str);
    }
}

private static void solution(String input) {
    String fixed = input.replaceAll("[0-9]|[a-z]", "");
    if (fixed.length() > 0) {
        System.out.println("!error");
        return;
    }

    StringBuilder res = new StringBuilder();
    int count = 1;
    char[] chars = input.toCharArray();
    for (int i = 0; i < chars.length; i++) {
        if (Character.isLetter(chars[i])) {
            // 筛选到字母字符时
            for (int j = 0; j < count; j++) {
                res.append(chars[i]);
            }
            count = 1;
        } else {
            // 筛选到数字字符时
            int pos = i;
            while (Character.isDigit(chars[i])) {
                i++;
            }
            if (i > pos) {
                count = Integer.parseInt(input.substring(pos, i--));
            }
            if (count == 2){
                System.out.println("!error");
                return;
            }
        }
    }
    System.out.println(res);
}
```



### 12.【数字的反转打印】

> 小华是个很有对数字很敏感的小朋友，他觉得数字的不同排列方式有特殊美感。某天，小华突发奇想，如果数字多行排列，第一行1个数，第二行2个，第三行3个，即第n行有n个数字，并且奇数行正序排列，偶数行逆序排列，数字依次累加。这样排列的数字一定很有意思。聪明的你能编写代码帮助小华完成这个想法吗？
> 规则总结如下：
>
> a、每个数字占据4个位置，不足四位用‘*’补位，如1打印为1***。
>
> b、数字之间相邻4空格。
>
> c、数字的打印顺序按照正序逆序交替打印,奇数行正序，偶数行逆序。
>
> d、最后一行数字顶格，第n-1行相对第n行缩进四个空格
> ```
> 输入描述:
> 
> 第一行输入为N，表示打印多少行; 1<=N<=30
> 
> 输入：2
> 
> 输出描述:
> 
> XXXX1***
> 
> 3***XXXX2***
> 示例1
> 输入
> 2
> 
> 输出
> 
> 1***
> 
> 3***   2***
> 
> 备注:
> 
> 符号*表示，数字不满4位时的补位，符号X表示数字之间的空格。注意实际编码时不需要打印X，直接打印空格即可。此处为说明题意，故此加上X
> ```
>
> 

思路:

> 根据题目所示，得出的数据应该如下图所示：
>
> ​      1***
>
> ​    3***  2***
>
> 4***  5***  6***
>
>   10**  9***  8***  7***
>
> ........................................
>
> 从上图可以得到规律：
>
> 第n行的最小数字 = 第n-1行的最小数字+第n-1行的行数（n-1）
>
> 得到n行的最小数字之后再通过n次递增，就会获取n行的所有数字

```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String str;
    while ((str = br.readLine()) != null) {
        int n = Integer.parseInt(str);
        solution(n);
    }
}

private static String handle(Integer num) {
    StringBuilder sb = new StringBuilder();
    sb.append(num);
    for (int j = (num + "").length(); j < 4; j++) {
        sb.append("*");
    }
    return sb.toString();
}

private static void solution(int n) {
    List<List<String>> list = new ArrayList<>();
    int num = 1;
    for (int i = 1; i <= n; i++) {
        List<String> tmpList = new ArrayList<>();
        for (int j = 0; j < i; j++) {
            tmpList.add(handle(num++));
        }
        list.add(tmpList);
    }
    for (int i = 0; i < list.size(); i++) {
        for (int j = 1; j < list.size() - i; j++) {
            System.out.print("    ");
        }
        List<String> strings = list.get(i);
        if ((i + 1) % 2 == 0) {
            for (int k = strings.size() - 1; k >= 0; k--) {
                System.out.print(strings.get(k) + "    ");
            }
        } else {
            for (int k = 0; k < strings.size(); k++) {
                System.out.print(strings.get(k) + "    ");
            }
        }
        System.out.println();
    }
}
```

