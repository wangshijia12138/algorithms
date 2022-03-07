

### 题目一  【非严格递增连续数字序列】

>输入一个字符串仅包含大小写字母和数字，求字符串中包含的最长的非严格递增连续数字序列的长度（比如12234属于非严格递增连 续数字序列）。
>输入描述：
>输入一个字符串仅包含大小写字母和数字，输入的字符串最大不超过255个字符。
>输出描述：
>最长的非严格递增连续数字序列的长度
>
>示例1：
>输入：
>abc2234019A334bc
>输出：
>4


```java
 public static int solution1(String str) {
     int[] dp = new int[str.length()];
     if (Character.isAlphabetic(str.charAt(0))) {
         dp[0] = 0;
     } else {
         dp[0] = 1;
     }
     for (int i = 1; i < str.length(); i++) {
         if (Character.isAlphabetic(str.charAt(i))) {
             dp[i] = 0;
             continue;
         }
         if (Character.isAlphabetic(str.charAt(i - 1)) || str.charAt(i) < str.charAt(i - 1)) {
             dp[i] = 1;
         } else {
             dp[i] = dp[i - 1] + 1;
         }
     }
     Arrays.sort(dp);
     return dp[dp.length - 1];
 }
```

### 题目二   【工号不够用了怎么办？】

>3020年，空间通信集团的员工人数突破20亿人，即将遇到现有工号不够用的窘境。
>现在，请你负责调研新工号系统。继承历史传统，新的工号系统由小写英文字母（a-z）和数字（0-9）两部分构成。
>新工号由一段英文字母开头，之后跟随一段数 字，比如"aaahw0001","a12345","abcd1","a00"。
>注意新工号不能全为字母或者数字,允许数字部分有前导0或者全为0。 但是过长的工号会增加同事们的记忆成本，
>现在给出新工号至少需要分配的人数X和新工号中字母的长度Y，求新工号中数字的最短长度Z。
>输入描述：
>一行两个非负整数 X Y，用数字用单个空格分隔。
>0< X <=2^50 – 1
>0< Y <=5
>输出描述：
>输出新工号中数字的最短长度Z
>
>示例1：
>输入：
>260 1
>输出：
>1

```java
 public static void main(String[] args) throws IOException {
     BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
     String str;
     while ((str = br.readLine()) != null) {
         String[] s = str.split(" ");
         int x = Integer.parseInt(s[0]);
         int y = Integer.parseInt(s[1]);
         System.out.println(solution2(x, y));
     }
 }

 public static int solution2(int x, int y) {
     double v = x * 1.0 / Math.pow(26, y);
     int count = 1;
     while (v > 10) {
         count++;
         v = v / 10;
     }

     return count;
 }
```



### 题目三   【火锅】

>入职后，导师会请你吃饭，你选择了火锅。 火锅里会在不同时间下很多菜。
>不同食材要煮不同的时间，才能变得刚好合适。你希望吃到最多的刚好合适的菜，
>但是你的手速不够快，用m代表手速，每次下手捞菜后至少要过m秒才能再捞（每次只能捞一个）。 那么用最合理的策略，最多能吃到多少刚好合适的菜？
>输入描述：
>第一行两个整数n，m，其中n 代表往锅里下的菜的个数，m 代表手速。
>接下来有n行，每行有两个数x，y 代表第x秒下的菜过y秒才能变得刚好合适。
> (1 < n,m < 1000)
>(1 <x, y<1000)
>输出描述：
>输出一个整数代表用最合理的策略，最多能吃到刚好合适的菜的数量
>
>示例1：
>输入：
>3 10
>1 5
>2 1
>5 10
>输出：
>1

```java
 public static void main(String[] args) throws IOException {
     BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
     String str;
     while ((str = br.readLine()) != null) {
         String[] s = str.split(" ");
         int dishes = Integer.parseInt(s[0]);
         int speed = Integer.parseInt(s[1]);
         int[] ints = new int[dishes];
         for (int i = 0; i < dishes; i++) {
             String[] s1 = br.readLine().split(" ");
             int x = Integer.parseInt(s1[0]);
             int y = Integer.parseInt(s1[1]);
             ints[i] = x + y;
         }
         Arrays.sort(ints);

         int count = 1;
         int cur = 0;
         for (int i = 1; i < ints.length; i++) {
             if (ints[i] - ints[cur] >= speed) {
                 count++;
                 cur = i;
                 continue;
             }
             while (i < ints.length && (ints[i] - ints[cur] < speed)) {
                 i++;
             }
             if (i >= ints.length) {
                 break;
             }
             count++;
             cur = i;
         }
         System.out.println(count);
     }
 }
```













