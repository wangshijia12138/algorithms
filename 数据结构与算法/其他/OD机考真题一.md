## 题目一  【热点网站统计】
***

>企业路由器的统计页面，有一个功能需要动态统计公司访问最多的网页URL top N。请设计一个算法，可以高效动态统计Top N的页面。
>输入描述：
>每一行都是一个URL或一个数字，如果是URL，代表一段时间内的网页访问；
>如果是一个数字N，代表本次需要输出的Top N个URL。
>输入约束：
>1、总访问网页数量小于5000个，单网页访问次数小于65535次；
>   2、网页URL仅由字母，数字和点分隔符组成，且长度小于等于127字节；
>   3、数字是 正整数，小于等于10且小于当前总访问网页数；
>输出描述：
>每行输入要对应一行输出，输出按访问次数排序的前N个URL，用逗号分隔。
>输出要求：
>1、每次输出要统计之前所有输入，不仅是本次输入；如果有访问次数相等的URL，
>   按URL的字符串字典序升序排列，输出排序靠前的URL；
>
>```
>示例1：
>输入：
>news.qq.com 
>news.sina.com
>news.qq.com
>news.qq.com
>game.163.com
>game.163.com
>www.huawei.com
>www.cctv.com
>3
>www.huawei.com
>www.cctv.com
>www.huawei.com
>www.cctv.com
>www.huawei.com
>www.cctv.com
>www.huawei.com
>www.cctv.com
>www.huawei.com
>3
>输出：
>news.qq.com,game.163.com,news.sina.com.cn
>www.huawei.com,www.cctv.com,news.qq.com
>```


```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.HashMap;
import java.util.Map;
import java.util.Objects;
import java.util.regex.Pattern;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str1;
        Map<String, Integer> map = new HashMap<>();
        while ((str1 = br.readLine()) != null) {
            // 校验为url时 ,map入库
            if (Pattern.matches("^[A-Za-z0-9]+.[A-Za-z0-9]+.com|cn$", str1)) {
                map.put(str1, map.getOrDefault(str1, 0) + 1);
            } else {
                // 非url时,进行排序统计
                int count = Integer.parseInt(str1);
                ArrayList<Map.Entry<String, Integer>> list = new ArrayList<>(map.entrySet());
                list.sort(new Comparator<Map.Entry<String, Integer>>() {
                    @Override
                    public int compare(Map.Entry<String, Integer> o1, Map.Entry<String, Integer> o2) {
                        if (Objects.equals(o2.getValue(), o1.getValue())) {
                            return o1.getKey().compareTo(o2.getKey());
                        } else {
                            return o2.getValue() - o1.getValue();
                        }
                    }
                });
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < 3; i++) {
                    sb.append(list.get(i).getKey()).append(",");
                }
                sb.deleteCharAt(sb.length() - 1);
                System.out.println(sb);
            }
        }
    }
```

## 题目二   【最大差】

***

>判断一组不等式是否满足约束并输出
>
>给定一组不等式，判断是否成立并输出不等式的最大差(输出浮点数的整数部分)， 要求：
>
>1）不等式系数为double类型，是一个二维数组；
>
>2）不等式的变量为int类型，是一维数组；
>
>3）不等式的目标值为double类型，是一维数组；
>
>4）不等式约束为字符串数组，只能是：">",">=","<","<=","="，例如,不等式组：
>
>a11*x1+a12*x2+a13*x3+a14*x4+a15*x5<=b1;a21*x1+a22*x2+a23*x3+a24*x4+a25*x5<=b2;a31*x1+a32*x2+a33*x3+a34*x4+a35*x5<=b3;
>最大差=max{ (a11*x1+a12*x2+a13*x3+a14*x4+a15*x5-b1),  (a21*x1+a22*x2+a23*x3+a24*x4+a25*x5-b2),(a31*x1+a32*x2+a33*x3+a34*x4+a35*x5-b3) }，
>
>类型为整数(输出浮点数的整数部分)
>
>```
>**输入描述**:
>
>1）不等式组系数(double类型)：
>
>a11,a12,a13,a14,a15 a21,a22,a23,a24,a25 a31,a32,a33,a34,a35
>
>2）不等式变量(int类型)：
>
>x1,x2,x3,x4,x5
>
>3）不等式目标值(double类型)：b1,b2,b3
>
>4)不等式约束(字符串类型):<=,<=,<=
>
>**输入：**
>
>a11,a12,a13,a14,a15;
>
>a21,a22,a23,a24,a25;
>
>a31,a32,a33,a34,a35;
>
>x1,x2,x3,x4,x5;
>
>b1,b2,b3;
>
><=,<=,<=
>
>**输出描述:**
>
>true 或者 false, 最大差
>
>示例1：
>输入：
>2.3,3,5.6,7,6;11,3,8.6,25,1;0.3,9,5.3,66,7.8;1,3,2,7,5;340,670,80.6;<=,<=,<=
>输出：
>false 458
>```

```java
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str1;
        while ((str1 = br.readLine()) != null) {
            // 解析系数
            String[] split = str1.split(";");
            int size = split[0].split(",").length;
            double[][] coefficient = new double[3][size];
            for (int i = 0; i < 3; i++) {
                String[] temp1 = split[i].split(",");
                for (int j = 0; j < coefficient[i].length; j++) {
                    coefficient[i][j] = Double.parseDouble(temp1[j]);
                }
            }

            // 解析变量
            String[] temp2 = split[3].split(",");
            int[] value = new int[temp2.length];
            for (int i = 0; i < value.length; i++) {
                value[i] = Integer.parseInt(temp2[i]);
            }

            // 解析目标值
            String[] temp3 = split[4].split(",");
            double[] res = new double[temp3.length];
            for (int i = 0; i < res.length; i++) {
                res[i] = Double.parseDouble(temp3[i]);
            }
            // 解析符号
            String[] symbol = split[5].split(",");

            double max = Double.MIN_VALUE;
            boolean flag = true;
            for (int i = 0; i < coefficient.length; i++) {
                double sum = 0;
                for (int j = 0; j < coefficient[i].length; j++) {
                    sum = sum + coefficient[i][j] * value[j];
                }
                max = Math.max(sum - res[i], max);
                if (!check(symbol[i], sum, res[i])) {
                    flag = false;
                }
            }
            System.out.println(flag + " " + (int) max);
        }
    }

    private static boolean check(String symbol, double sum, double res) {
        boolean check = false;
        switch (symbol) {
            case ">":
                check = sum > res;
                break;
            case ">=":
                check = sum >= res;
                break;
            case "<":
                check = sum < res;
                break;
            case "<=":
                check = sum <= res;
                break;
            case "=":
                check = sum == res;
                break;
            default:
                break;
        }
        return check;
    }
```



## 题目三  【二叉树的广度优先遍历】
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

```java
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String str;
        while ((str = br.readLine()) != null) {
            String[] s = str.split(" ");
            System.out.println(solution(s[1], s[0]));
        }
    }

    public static class TreeNode {
        String val;
        TreeNode left;

        TreeNode right;

        TreeNode() {
        }

        TreeNode(String val) {
            this.val = val;
        }

        TreeNode(String val, TreeNode left, TreeNode right) {
            this.val = val;
            this.left = left;
            this.right = right;
        }
    }



    public static String solution(String inorder, String postorder) {
        return levelOrder(buildTree(inorder, postorder));
    }
    
    public static TreeNode buildTree(String inorder, String postorder) {
        if (inorder.length() == 0 || postorder.length() == 0) {
            return null;
        }
        char root = postorder.charAt(postorder.length() - 1);
        Integer rootIndex = inorder.indexOf(root);
        String leftInorder = inorder.substring(0, rootIndex);
        String rightInorder = inorder.substring(rootIndex + 1);
        String leftPostorder = postorder.substring(0, leftInorder.length());
        String rightPostorder = postorder.substring(leftInorder.length(),postorder.length() - 1);
        TreeNode treeNode = new TreeNode(root + "");
        treeNode.left = buildTree(leftInorder, leftPostorder);
        treeNode.right = buildTree(rightInorder, rightPostorder);
        return treeNode;
    }

    public static String levelOrder(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        ArrayDeque<TreeNode> queue = new ArrayDeque<>();
        if (root != null) {
            queue.add(root);
        }
        while (!queue.isEmpty()) {
            int n = queue.size();
            for (int i = 0; i < n; i++) {
                TreeNode poll = queue.poll();
                sb.append(poll.val);
                if (poll.left != null) {
                    queue.add(poll.left);
                }
                if (poll.right != null) {
                    queue.add(poll.right);
                }
            }
        }
        return sb.toString();
    }
```

