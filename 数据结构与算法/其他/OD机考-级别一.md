### 级别一  【消消乐游戏】

>游戏规则：
>输入一个只包含英文字母的字符串
>字符串中的两个字母如果相邻且相同,就可以消除。
>在字符串上反复执行消除的动作,
>直到无法继续消除为止,此时游戏结束。
>输出最终得到的字符串长度
>
>输入描述：
>输入原始字符串str
>只能包含大小写英文字母,字母的大小写敏感,
>str长度不超过100
>
>输出描述
>输出游戏结束后,最终得到的字符串长度
>
>```
> 示例一：
>  输入
>    gg
>
>  输出
>    0
>    说明 gg可以直接消除 得到空串 长度为0
>
>  示例2
>  输入：
>    mMbccbc
>    0123456
>  输出
>    3
>   说明mMbccbc中 可以先消除cc 此时变为mMbbc
>   再消除 bb 此时变成mMc
>   此时没有相同且相邻的字符 无法继续消除
>   最终得到字符串mMc  长度为3
>
>  备注：
>   输入中包含非大小写英文字母时
>   均为异常输入
>   直接返回0
>```

思路:

>1.暴力法,通过递归不断处理重复的英文字母,直到最后字符串中不存在重复的相邻字母 (×)
>
>2.通过构建一个链表结构,不断向内输入字符,出现重复字符消除  (√)



```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String str;
    while ((str = br.readLine()) != null) {
        solution(str);
    }
}

//通过构建一个链表结构,不断向内输入字符,出现重复字符消除
private static void solution(String input) {
    if (!Pattern.matches("^[a-zA-Z]+$", input)) {
        System.out.println(0);
        return;
    }
    LinkedList<Character> list = new LinkedList<>();
    for (int i = 0; i < input.length(); i++) {
        if (list.size() < 1) {
            list.add(input.charAt(i));
            continue;
        }
        if (input.charAt(i) == list.getLast()) {
            list.removeLast();
        } else {
            list.add(input.charAt(i));
        }
    }
    System.out.println(list.size());
}
```



### 级别一   【最大花费金额】

>双11众多商品进行打折销售，小明想购买一些自己心意的商品
>但由于受购买资金限制，所以他决定从众多心意商品中购买3件
>而且想尽可能的花完资金
>现在请你设计一个程序帮助小明计算尽可能花费的最大资金额
>
>输入描述
>第一行为整型数组M 数组长度小于100 数组元素记录单个商品的价格
>单个商品价格<1000
>第二行输入为购买资金的额度R
>R<100000
>
>输出描述
>输出为满足上述条件的最大花费额度
>如果不存在满足上述条件的商品请返回-1
>
>```
>例子1
>输入
> 23,26,36,27
> 78
>输出
> 76
>
>例子2
>    输入
>     23,30,40
>     26
>    输出
>      -1
>
>备注：输入格式正确
>```

思路:

>1. 穷举所有可能,取数额最大的那个金额

```java
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str;
        while ((str = br.readLine()) != null) {
            String[] split = str.split(",");
            int[] values = new int[split.length];
            for (int i = 0; i < split.length; i++) {
                values[i] = Integer.parseInt(split[i]);
            }
            int money = Integer.parseInt(br.readLine());
            solution(values, money);
        }
    }

    private static void solution(int[] values, int money) {
        TreeSet<Integer> set = new TreeSet<>();
        for (int i = 0; i < values.length; i++) {
            for (int j = i + 1; j < values.length; j++) {
                for (int k = j + 1; k < values.length; k++) {
                    int all = values[i] + values[j] + values[k];
                    if (all <= money) {
                        set.add(all);
                    }
                }
            }
        }
```

### 级别一    【快递运输】

>一辆运送快递的货车
>运送的快递放在大小不等的长方体快递盒中
>为了能够装载更多的快递同时不能让货车超载
>需要计算最多能装多少个快递
>注：快递的体积不受限制
>快递数最多1000个
>货车载重最大50000
>
>```
>输入描述
>第一行输入每个快递的重量
>用英文逗号隔开
>如 5,10,2,11
>第二行输入货车的载重量
>如 20
>
>输出描述
>输出最多能装多少个快递
>如 3
>示例一
>输入
>5,10,2,11
>20
>输出
>3
>说明
>货车的载重量为20，最多只能放三个快递5、10、2，因此输出3
>```

思路

>贪心算法,每次选最轻的快递

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
            Arrays.sort(ints);
            solution(ints, Integer.parseInt(br.readLine()));
        }
    }

    private static void solution(int[] ints, int max) {
        int sum = 0;
        for (int i = 0; i < ints.length; i++) {
            sum += ints[i];
            if (sum > max) {
                System.out.println(i);
                return;
            }
        }
        System.out.println(ints.length);
    }
```

### 级别一  【数列描述】

>有一个数列A[n]
>从A[0]开始每一项都是一个数字
>数列中A[n+1]都是A[n]的描述
>其中A[0]=1
>规则如下
>A[0]:1
>A[1]:11
>含义其中A[0]=1是1个1 即11
>表示A[0]从左到右连续出现了1次1
>
>A[2]:21
>含义其中A[1]=11是2个1 即21
>表示A[1]从左到右连续出现了2次1
>
>A[3]:1211
>含义其中A[2]从左到右是由一个2和一个1组成 即1211
>表示A[2]从左到右连续出现了一次2又连续出现了一次1
>
>A[4]:111221
>含义A[3]=1211 从左到右是由一个1和一个2两个1 即111221
>表示A[3]从左到右连续出现了一次1又连续出现了一次2又连续出现了2次1
>
>```
>输出第n项的结果
>0<= n <=59
>输入描述：
>数列第n项 0<= n <=594
>输出描述
>数列内容
>111221
>```

思路:

>基于动态规划的思想实现, A[n] = f(A[n-1])  关键点是如何构建两者之前的转化函数

```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String str;
    while ((str = br.readLine()) != null) {
        int n = Integer.parseInt(str);
        solution(n);
    }
}

private static void solution(int n) {
    if (n <= 1) {
        System.out.println(1);
    }
    String[] array = new String[n];
    array[0] = "1";
    for (int i = 1; i < array.length; i++) {
        array[i] = f(array[i - 1]);
    }
    System.out.println(array[n - 1]);
}

private static String f(String num) {
    int count = 1;
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < num.length(); i++) {
        if (i != num.length() - 1 && num.charAt(i) == num.charAt(i + 1)) {
            count++;
        } else {
            sb.append(count).append(num.charAt(i));
            count = 1;
        }
    }
    return sb.toString();
}
```



### 【最长元音字串的长度】

>定义当一个字符串只有元音字母(a,e,i,o,u,A,E,I,O,U)组成,
>称为元音字符串，现给定一个字符串，请找出其中最长的元音字符串，
>并返回其长度，如果找不到请返回0，
>字符串中任意一个连续字符组成的子序列称为该字符串的子串
>
>输入描述：
>一个字符串其长度 0<length ,字符串仅由字符a-z或A-Z组成
>输出描述：
>一个整数，表示最长的元音字符子串的长度
>
>```
>示例1：
>  输入
>    asdbuiodevauufgh
>  输出
>    3
>  说明：
>    最长的元音字符子串为uio和auu长度都为3，因此输出3
>```

思路:

>遍历每一个字符,遇到元音字符累加,非元音字符清零

```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String str;
    while ((str = br.readLine()) != null) {
        solution(str);
    }
}

private static void solution(String input) {
    List<Character> vowel = Arrays.asList('a', 'e', 'i', 'o', 'u');
    int max = 0;
    int count = 0;
    for (int i = 0; i < input.length(); i++) {
        char cur = input.charAt(i);
        if (vowel.contains(cur)) {
            count++;
        } else {
            max = Math.max(max, count);
            count = 0;
        }
    }
    System.out.println(max);
}
```



### 【员工考勤记录】

>公司用一个字符串来标识员工的出勤信息
>
>absent: 缺勤
>late: 迟到
>leaveearly:早退
>present: 正常上班
>
>现需根据员工出勤信息,判断本次是否能获得出勤奖,
>能获得出勤奖的条件如下：
>1.缺勤不超过1次
>2.没有连续的迟到/早退
>3.任意连续7次考勤 缺勤/迟到/早退 不超过3次
>
>输入描述：
>用户的考勤数据字符串记录条数 >=1
>输入字符串长度<10000 ;
>不存在非法输入
>如：
>2
>present
>present absent present present leaveearly present absent
>
>输出描述：
>根据考勤数据字符串
>如果能得到考勤奖输出true否则输出false
>对于输出示例的结果应为
>true false
>
>```
>例一：
> 输入：
>  2
>  present
>  present present
>
> 输出：
>  true true
>
>示例二
> 输入：
>  2
>  present
>  present absent present present leaveearly present absent
> 输出：
>  true false
>```

```java
public static void main(String[] args) throws IOException {
    BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
    String str;
    while ((str = br.readLine()) != null) {
        int n = Integer.parseInt(str);
        String[] strs = new String[n];
        for (int i = 0; i < strs.length; i++) {
            strs[i] = br.readLine();
        }
        solution(strs);
    }
}

private static void solution(String[] strs) {
    for (String str : strs) {
        String[] s = str.split(" ");
        System.out.print(check(s) + " ");
    }
}

private static boolean check(String[] list) {
    int count1 = 0;
    int count2 = 0;
    int count3 = 0;
    for (int i = 0; i < list.length; i++) {
        String s = list[i];
        // 1.缺勤不超过1次
        if ("absent".equals(s)) {
            count1++;
        }
        if (count1 >= 2) {
            return false;
        }
        //  2.没有连续的迟到/早退
        if ("late".equals(s) || "leaveearly".equals(s)) {
            count2++;
        } else {
            count2 = 0;
        }
        if (count2 >= 2) {
            return false;
        }
        // 3.任意连续7次考勤 缺勤/迟到/早退 不超过3次
        if (list.length <= 7) {
            if ("absent".equals(s) || "late".equals(s) || "leaveearly".equals(s)) {
                count3++;
            }
            if (count3 >= 4) {
                return false;
            }
        } else {
            for (int j = i; j < 7 + i; j++) {
                String t = list[j];
                if ("absent".equals(t) || "late".equals(t) || "leaveearly".equals(t)) {
                    count3++;
                }
                if (count3 >= 4) {
                    return false;
                }
            }
        }
    }
    return true;
}
```



### 【找车位】

>停车场有一横排车位0代表没有停车,1代表有车.
>至少停了一辆车在车位上,也至少有一个空位没有停车.
>为防止刮蹭,需为停车人找到一个车位
>使得停车人的车最近的车辆的距离是最大的
>返回此时的最大距离
>
>输入描述:
>
>1. 一个用半角逗号分割的停车标识字符串,停车标识为0或1,
>     0为空位,1为已停车
>   2. 停车位最多有100个
>
>```
>输出描述
>  1. 输出一个整数记录最大距离
>
>  示例一:
>  输入
>  1,0,0,0,0,1,0,0,1,0,1
>
>   0,0,1,1,0,0
>  输出
>  2
>
>  说明
>  当车停在第三个位置上时,离其最近的车距离为2(1~3)
>  当车停在第四个位置上时,离其最近的车距离为2(4~6)
>  其他位置距离为1
>  因此最大距离为2
>```

## 

### 【找出第一次相同且连续的子串（字符串匹配）】

>给你两个字符串t和p
>要求从t中找到一个和p相同的连续子串
>并输出该子串第一个字符的下标
>输入描述
>输入文件包括两行 分别表示字符串t和p
>保证t的长度不小于p
>且t的长度不超过1000000
>p的长度不超过10000
>输出描述
>如果能从t中找到一个和p相等的连续子串,
>则输出该子串第一个字符在t中的下标
>下标从左到右依次为1,2,3,…；
>如果不能则输出 “No”
>如果含有多个这样的子串
>则输出第一个字符下标最小的
>
>```
>示例一：
>输入：
>AVERDXIVYERDIAN
>RDXI
>输出
>4
>```

