[1. 两数之和 - 力扣（LeetCode） (leetcode-cn.com)](https://leetcode-cn.com/problems/two-sum/)

```java
    public int[] twoSum(int[] nums, int target) {
        if (nums.length == 2 && nums[0] + nums[1] == target){
            return new int[]{0,1};
        }
        int[] res = new int[2];
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])){
                res[1] = i;
                res[0] = map.get(target - nums[i]);
                return res;
            }
            map.put(nums[i], i);
        }
        return res;
    }
```

