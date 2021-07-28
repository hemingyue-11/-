# LeetCode 15. 三数之和

![123](images\leetcode15.png)

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new LinkedList();
        if (nums.length < 3) return res;
        Arrays.sort(nums);//排序
        for (int i = 0; i<nums.length-1; i++) {
            if (nums[i] > 0) break; //如果当前数字大于0，说明三个数字之和一定大于0，结束循环
            if (i > 0 && nums[i] == nums[i-1]) continue; //去重
            int left = i + 1;
            int right = nums.length-1;
            while(left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum > 0) {
                    right--;

                } else if (sum < 0) {
                    left ++;
                } else {
                    while(left < right && nums[left] == nums[left + 1]) left++; //去重
                    while(left < right && nums[right] == nums[right - 1]) right--; //去重
                    res.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    left++;
                }
            }
        }
        return res;
    }
}

```

首先对数组进行排序，排序后就应该想到左右指针，首先固定第一个数 i ，然后在这个数的右面使用左右指针 i+1、length-1，如果这个数i大于0那么这三个数是不可能等于0的，这时候就应该跳出，使用左右指针时，当三个数的和大于0，右指针向左移，当和小于0时，左指针向右移，当等于0说明这个三元组符合条件。

本体中最困难的时对结果进行去重，当和为0时，如果左指针和左指针右边的数相等，说明这两组数是重复的，应该跳过，同理，右指针相似。
