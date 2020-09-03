```
A peak element is an element that is greater than its neighbors.
Given an input array nums, where nums[i] ≠ nums[i+1], find a peak element and return its index.
The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.
You may imagine that nums[-1] = nums[n] = -∞.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/find-peak-element
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
当然我只想到了线性遍历。
```
var findPeakElement = function(nums) {
    nums.unshift(-Infinity);
    nums.push(-Infinity);
    let n = nums.length;
    for(let i = 1; i < n - 1; i++){
        if(nums[i] > nums[i-1] && nums[i] > nums[i+1]){
            return i - 1;
        }
    }
};
```
没想到还可以用二分查找。
```
var findPeakElement = function(nums) {
    let left = 0;
    let right = nums.length - 1;
    while(left < right){
        let mid = Math.floor((left + right)/2);
        if(nums[mid] > nums[mid+1]){
            right = mid;
        }else{
            left = mid+1;
        }
    }
    return left;
};
```
