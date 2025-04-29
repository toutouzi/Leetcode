## 题目描述

给一个数n，一个数组A，返回由A中元素组成的小于n的最大数
如n=23121，A={2,4,9| 返回22999
n=23121 A={9} 返回9999
n=23333 A={2,3} 返回23332
n=2222 A={2} 返回222
n=2 A={2} 无解



## 代码

```java
import java.io.*;
import java.sql.SQLOutput;
import java.util.*;



public class Main {
    // 示例 1：A={1, 2, 9, 4}，n=2533，返回 2499。
    // 示例 2：A={1, 2, 5, 4}，n=2543，返回 2542。
    // 示例 3：A={1, 2, 5, 4}，n=2541，返回 2525。
    // 示例 4：A={1, 2, 9, 4}，n=2111，返回 1999。
    // 示例 5：A={5, 9}，n=5555，返回 999。


    public static void main(String[] args) {
//        case 1
//        int[] nums = new int[]{2, 4, 6, 8};
//        int n = 2411;

//        case 2
//        int[] nums = new int[]{9, 8, 7, 6};
//        int n = 2411;

//        case 3
//        int[] nums = new int[]{8, 7, 6};
//        int n = 2411;

//        case 4
        int[] nums = new int[]{4, 5, 6};
        int n = 23;

//        int[] nums = new int[]{2, 4, 6, 8};
//        int n = 2411;

//        int[] nums = new int[]{5,9};
//        int n = 5555;
        char[] s = Integer.toString(n - 1).toCharArray();
        StringBuilder sb = new StringBuilder();

        System.out.println(dfs(0, true, false, nums, s, sb,  0)); //2288
    }

    public static int dfs(int i, boolean isLimit, boolean isNum,int[] nums, char[] s, StringBuilder sb, int ans) {
        if (i == s.length) {           // 扫描完所有位
            if (isNum)  ans = Math.max(ans, Integer.valueOf(sb.toString()));
            return ans;
        }

        if (!isNum) {
            ans = Math.max(ans, dfs(i + 1, false, false, nums, s, sb, ans));
        }

        int up = isLimit ? s[i] - '0' : nums[nums.length - 1];
        for (int num : nums) {
            if (num > up) break;           // 剪枝
            sb.append(num);
            ans = Math.max(ans,dfs(i + 1, isLimit && num == up, true,nums, s, sb, ans));
            sb.deleteCharAt(sb.length() - 1);
        }

        return ans;


    }
}


```

