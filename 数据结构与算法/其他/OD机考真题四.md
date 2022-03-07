

## 

### 题目一  【探险队】

>某探险队负责对地下洞穴进行探险。探险队成员在进行探险任务时，随身携带的记录器会不定期地记录自身的坐标，
>但在记录的间隙中也会记录其他数据。探索工作 结束后，探险队需要获取到某成员在探险过程中相对于探险队总部的最远的足迹位置。
>
>1. 仪器记录坐标时，坐标的数据格式为(x,y)，如(1,2)、(100,200)，其中0<x<1000，0<y<1000。同时存在非法坐标，如(01,1)、(1,01)，(0,100)属于非法坐标。
>2. 设定探险队总部的坐标为(0,0)，某位置相对总部的距离为：x*x+y*y。
>3. 若两个座标的相对总部的距离相同，则第一次到达的坐标为最远的足迹。
>4. 若记录仪中的坐标都不合法，输出总部坐标（0,0）。
>     备注：不需要考虑双层括号嵌套的情况，比如sfsdfsd((1,2))。
>```
>输入描述：
>字符串，表示记录仪中的数据
>如：ferga13fdsf3(100,200)f2r3rfasf(300,400)
>输出描述：
>   字符串，表示最远足迹到达的坐标。
>     如： (300,400)
>     
>     示例1：
>   输入：
>     ferg(3,10)a13fdsf3(3,4)f2r3rfasf(05,10)
>   输出：
>     (5,10)
> ```


```java
 public static void main(String[] args) throws IOException {
     BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
     String str;
     while ((str = br.readLine()) != null) {
         StringBuilder sb = new StringBuilder();
         for (int i = 0; i < str.length(); i++) {
             char c = str.charAt(i);
             if (c == '(') {
                 i++;
                 while (i < str.length() && str.charAt(i) != ')') {
                     sb.append(str.charAt(i));
                     i++;
                 }
                 sb.append(" ");
             }
         }
         String[] coordinates = sb.toString().split(" ");
         double max = 0;
         int index = -1;
         for (int i = 0; i < coordinates.length; i++) {
             String[] split = coordinates[i].split(",");
             if (split[0].startsWith("0") || split[1].startsWith("0")) {
                 continue;
             }
             int a = Integer.parseInt(split[0]);
             int b = Integer.parseInt(split[1]);
             double abs = Math.sqrt(a * a + b * b);

             if (abs > max) {
                 max = abs;
                 index = i;
             }
         }
         if (index == -1) {
             System.out.println("(0,0)");
         } else {
             System.out.println("(" + coordinates[index] + ")");
         }
     }
 }
```

### 题目二   【喊7的次数重排】

>喊7是一个传统的聚会游戏，N个人围成一圈，按顺时针从1到N编号。编号为1的人从1开始喊数，下一个人喊的数字为上一个人的数字加1，
>但是当将要喊出来的数字是7的倍数或者数字本身含有7的话，不能把这个数字直接喊出来，而是要喊"过"。
>假定玩这个游戏的N个人都没有失误地在正确的时机喊了"过"，当喊到数字K 时，可以统计每个人喊"过"的次数。
>
>现给定一个长度为N的数组，存储了打乱顺序的每个人喊"过"的次数，请把它还原成正确的顺序，即数组的第i个元素存储编号i的人喊"过"的次数。
>
>输入描述：
>输入为一行，为空格分隔的喊"过"的次数，注意K并不提供，K不超过200，而数字的个数即为N。
>输出描述：
>输出为一行，为顺序正确的喊"过"的次数，也由空格分隔。
>
>```
>示例1：
>输入：
>0 1 0
>输出：
>1 0 0
>```

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



### 题目三 【数字排列】

>小明负责公司年会，想出一个趣味游戏： 屏幕给出1～9中任意4个不重复的数字，
>大家以最快时间给出这几个数字可拼成的数字从小到大排列位于第N位置的数字，
>其中N为给出的数字中最大的（如果不到 这么多个数字则给出最后一个即可）。
>注意：
>1）2可以当做5来使用，5也可以当做2来使用进行数字拼接，且屏幕不能同时给出2和5；
>2）6可以当做9来使用，9也可以当做6来使用进行数字拼接，且屏幕不能同时给出6和9。
>如给出：1，4，8，7则可以拼成的数字为： 1，4，7，8，14，17，18，41，47，48，71，74，78，81，84，87，147，148，178...（省略后面的数字
>那么第N（即8）个的数字为41。
>
>输入描述：
>输入为以逗号分隔的描述4个int类型整数的字符串。
>输出描述：
>输出为这几个数字可拼成的数字从小到大排列位于第N（N为输入数字中最大的数字）位置的数字，如果输入的数字不在范围内或者有重复，则输出-1。
>
>```
>示例1：
>输入：
>1,4,8,7
>输出：
>41
>```
>
>

```

```

