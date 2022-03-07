

### 题目一  【消消乐游戏】

>游戏规则：输入一个只包含英文字母的字符串，字符串中的两个字母如果相邻且相同，就可以消除。 在字符串上反复执行消除的动作，直到无法继续消除为止，此时游戏结束。 输出最终得到的字符串长度
>输入描述：
>输入原始字符串 str ，只能包含大小写英文字母，字母的大小写敏感， str 长度不超过100。输出描述：
>输出游戏结束后，最终得到的字符串长度
>备注：
>   输入中包含 非大小写英文字母 时，均为异常输入，直接返回 0
>     
>      示例1：
>      输入：
>    gg
>      输出：
>    0


```java
 public static void main(String[] args) throws IOException {
     BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
     String str1;
     while ((str1 = br.readLine()) != null) {
         if (!Pattern.matches("^[a-zA-Z]+$", str1)) {
             System.out.println(0);
         }
         System.out.println(game(str1));
     }
 }

 public static int game(String str) {
     int change = 0;
     StringBuilder sb = new StringBuilder(str);
     for (int i = sb.length() - 1; i >= 1; i--) {
         char c1 = sb.charAt(i);
         char c2 = sb.charAt(i - 1);
         if (c1 == c2) {
             sb.deleteCharAt(i);
             sb.deleteCharAt(i - 1);
             i--;
             change++;
         }
     }
     if (change > 0) {
         return game(sb.toString());
     }
     return sb.length();
 }
```

### 题目二   【找终点】

>
>给定一个正整数数组，设为nums，最大为100个成员，求从第一个成员开始，正好走到数组最后一个成员，所使用的最少步骤数。
>要求：
>1、第一步必须从第一元素开始，且1<=第一步的步长<len/2;（len为数组的长度，需要自行解析）。
>2、从第二步开始，只能以所在成员的数字走相应的步数，不能多也不能少, 如果目标不可达返回-1，只输出最少的步骤数量。
>3、只能向数组的尾部走，不能往回走。
>输入描述：
>由正整数组成的数组，以空格分隔，数组长度小于100，请自行解析数据数量。
>
>输出描述：
>正整数，表示最少的步数，如果不存在输出-1
>
>示例1：
>输入：
>7 5 9 4 2 6 8 3 5 4 3 9
>输出：
>2

```java
 public static void main(String[] args) throws IOException {
     BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
     String str1;
     while ((str1 = br.readLine()) != null) {
         String[] s = str1.split(" ");
         int[] nums = new int[s.length];
         for (int i = 0; i < nums.length; i++) {
             nums[i] = Integer.parseInt(s[i]);
         }
         System.out.println(solution(nums));
     }
 }

 public static int solution(int[] nums) {
     int sum = 0;
     int min = Integer.MAX_VALUE;
     boolean flag = false;
     for (int i = 1; i <= nums.length / 2; i++) {
         int count = 2;
         sum = nums[0] + i;
         while (sum < nums.length) {
             sum = sum + nums[sum];
             count++;
         }
         if (sum == nums.length) {
             flag = true;
             min = Math.min(min, count);
         }
     }
     if (flag) {
         return min;
     } else {
         return -1;
     }
 }
```



### 题目三   【分月饼】

>题目描述： 中秋节，公司分月饼，m个员工，买了n个月饼，m<=n，每个员工至少分1个月饼，但可以分多个，单人分到最多月饼的个数是Max1，单人分到第二多月饼个数 是Max2，Max1-Max2 <= 3，单人分到第n-1多月饼个数是Max(n-1)，单人分到第n多月饼个数是Max(n)，Max(n-1) – Max(n) <= 3, 问有多少种分月饼的方法？
>
>输入描述：
>每一行输入m n，表示m个员工，n个月饼，m<=n
>
>输出描述：
>输出有多少种月饼分法
>
>示例1：
>输入：
>2 4
>输出：
>2

```

```















