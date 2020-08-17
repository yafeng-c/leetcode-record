```
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]

Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/move-zeroes
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
我真的想不到这个题还可以用双指针解，还这么巧妙。
```
var moveZeroes = function(nums) {
    let j = 0;
    for(let i = 0; i < nums.length; i++){
        if(nums[i] !== 0){
            if(i > j){//避免了开头元素非零，自己和自己交换的情况
                nums[j] = nums[i];
                nums[i] = 0;
                j++;
            }
        }
    }
    return nums;
};
```
