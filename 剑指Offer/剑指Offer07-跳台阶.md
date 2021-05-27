# 题目描述
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

# 思路及解法

使用递归即可，第1级台阶是1次，跳上第二级台阶可以选择从0直接跳到2，也可以从1跳到2。其他情况，我们可以归纳出，要想跳到n级台阶，最后一步有两种跳法，一种是从n-1级一次跳一级，一种是从n-2级一次跳两级。

```java
public class Solution {
    public int jumpFloor(int target) {
        if (target == 1) {
            return 1;
        } else if (target == 2) {
            return 2;
        } else {
            return jumpFloor(target - 1) + jumpFloor(target - 2);
        }
    }
}
```

但是这样会需要多次重复计算，我们可以利用数组将前面的结果存起来，计算的时候直接取出。

```java
public class Solution {
    public int jumpFloor(int target) {
    if (target == 1) {
            return 1;
     } else if (target == 2) {
            return 2;
     }
        int[] nums = new int[target + 1];
        nums[0] = 1;
        nums[1] = 2;
        for (int i = 2; i <= target; i++) {
            nums[i] = nums[i - 1] + nums[i - 2];
        }
        return nums[target-1];
    }
}
```

