[349. 两个数组的交集 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

```java
    public int[] intersection(int[] nums1, int[] nums2) {
        if (nums1.length >= nums2.length) {
            return solution(nums1, nums2);
        } else {
            return solution(nums2, nums1);
        }
    }

    private int[] solution(int[] nums1, int[] nums2) {
        HashSet<Integer> res = new HashSet<>();
        Set<Integer> set1 = convertArrayToSet(nums1);
        for (int num : nums2) {
            if (set1.contains(num)) {
                res.add(num);
            }
        }
        int[] ints = new int[res.size()];
        int i = 0;
        for (Integer re : res) {
            ints[i] = re;
            i++;
        }
        return ints;
    }

    private Set<Integer> convertArrayToSet(int[] nums) {
        HashSet<Integer> res = new HashSet<>();
        for (int num : nums) {
            res.add(num);
        }
        return res;
    }
```

