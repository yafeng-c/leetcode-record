```
Given an array, rotate the array to the right by k steps, where k is non-negative.

Follow up:
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
Could you do it in-place with O(1) extra space?
 

Example 1:
Input: nums = [1,2,3,4,5,6,7], k = 3
Output: [5,6,7,1,2,3,4]

Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]

Example 2:
Input: nums = [-1,-100,3,99], k = 2
Output: [3,99,-1,-100]

Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
 

Constraints:
1 <= nums.length <= 2 * 10^4
It's guaranteed that nums[i] fits in a 32 bit-signed integer.
k >= 0

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/rotate-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

当然我只想到了暴力解法。
官方题解里的环状替换描述非常抽象。这篇博客可以帮助理解：https://www.cnblogs.com/zhang-qi123/p/12296135.html

```
var rotate = function(nums, k) {
    let count = 0
    k = k % nums.length;
    for(start = 0; count < nums.length; start++){
        let currentIndex = start;
        let currentItem = nums[start];
        do{
            let nextIndex = (currentIndex + k) % nums.length;
            let nextItem = nums[nextIndex];
            nums[nextIndex] = currentItem;
            currentItem = nextItem;
            currentIndex = nextIndex;
            count++;
        }while(start != currentIndex)
    }
    return nums;
};
```
