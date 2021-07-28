# LeetCode 1. 两数之和

![](images/leetcode01.PNG)

## 题解

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> map = new HashMap();
        int[] res = new int[2];
        for (int i = 0; i<nums.length; i++) {
            if (map.containsKey(target-nums[i])){
                res[0] = map.get(target-nums[i]);
                res[1] = i;
            }
            map.put(nums[i], i);
        }
        return res;
    }
}
```

首先想到的是暴力破解，即对于每个树都从数组中查找是否存在target-nums[i]，但是复杂度是n2;

第二种方法是使用HashMap，遍历一次数组，对于每个nums[i]，我们现在map中查看是否有target-nums[i]，如果存在就说明找到了一对答案，将结果返回。如果不存在我们就将nums[i]作为key，i作为value插入map，因为需要返回nums[i]的索引。

