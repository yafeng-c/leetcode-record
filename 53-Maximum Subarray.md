```
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.

Follow up:
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/maximum-subarray
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
非常典型的动态规划问题，do[i]表示包含位置i可能出现的连续子串的最大值。
```
let dp = new Array(nums.length).fill(-Infinity);
    dp[0] = nums[0];
    for(let i = 1; i < nums.length; i++){
        if(dp[i-1] >= 0){
            dp[i] = dp[i-1] + nums[i];
        }else{
            dp[i] = Math.max(dp[i], nums[i])
        }
    }
    return Math.max(...dp)
```
由于最后只需要返回最大值，可以不用单纯创建数组存储，在遍历每个元素时，比较ans和sum。
```
var maxSubArray = function(nums) {
    let ans = nums[0];
    let sum = 0;
    for(let num of nums){
        if(sum <= 0){
            sum = num;
        }else{
            sum = sum + num;
        }
        ans = Math.max(ans, sum)
    }
    return ans;
};
```
但是实际内存消耗和方法一一样，时间还要慢一点，方法一80ms，而方法二92ms。方法二的思路曾经用Java写，运行只需要1ms，内存消耗也小一点。JS真的比Java慢很多。
