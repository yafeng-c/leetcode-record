```
Given an array nums with n integers, your task is to check if it could become non-decreasing by modifying at most 1 element.
We define an array is non-decreasing if nums[i] <= nums[i + 1] holds for every i (0-based) such that (0 <= i <= n - 2). 

Example 1:
Input: nums = [4,2,3]
Output: true
Explanation: You could modify the first 4 to 1 to get a non-decreasing array.

Example 2:
Input: nums = [4,2,1]
Output: false
Explanation: You can't get a non-decreasing array by modify at most one element.
 
Constraints:
1 <= n <= 10 ^ 4
- 10 ^ 5 <= nums[i] <= 10 ^ 5

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/non-decreasing-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
```
var checkPossibility = function(nums) {
    let count = 0;
    for(let i = 0; i < nums.length - 1; i++){
        if(nums[i] > nums[i+1]){
            count++;
        }
    }
    return count <= 1;
};
```
只是统计拐点次数无法通过类似[3,4,2,3]的输入。
因此，需要每次统计拐点后，同时改变数组拐点元素，使得当前位置满足非递减的条件。再进行下一个拐点的搜寻。
```
var checkPossibility = function(nums) {
    let count = 0;
    for(let i = 1; i < nums.length; i++){
        if(nums[i-1] > nums[i]){
            count++;
            if(count >= 2) return false;
            if(i-2>=0 && nums[i-2] > nums[i]){
                nums[i] = nums[i-1];
            }else{
                nums[i-1] = nums[i];
            }
        }
    }
     return true;
};
```
