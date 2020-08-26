```
In a given integer array nums, there is always exactly one largest element.

Find whether the largest element in the array is at least twice as much as every other number in the array.

If it is, return the index of the largest element, otherwise return -1.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/largest-number-at-least-twice-of-others
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
遍历两边很容易实现。遍历一次可以通过维护一个最大和一个次大的数。当然用JS内置函数比如indexof可以让代码更简洁。这里只是为了展示通用思路。
```
var dominantIndex = function(nums) {
    let max1 = 0, max2 = 0, index = 0;
    for(let i = 0; i < nums.length; i++){
        if(nums[i] > max1){
            max2 = max1;
            max1 = nums[i];
            index = i;
        }else if(nums[i] > max2){
            max2 = nums[i]
        }
    }
    if(max1 >= 2*max2) return index;
    return -1;
};
```
