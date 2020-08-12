```
Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.
The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.

Note:
Your returned answers (both index1 and index2) are not zero-based.
You may assume that each input would have exactly one solution and you may not use the same element twice.

Example:
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
由于数组已经排序，可以遍历每个元素并搜索能与当前元素组成目标值的下一个元素。这是暴力解法。
另一个方法利用了双指针。如果两个指针指向的元素和小于目标值，说明需要更大的元素相加，利用数组升序的特点，将左指针向后移动。同理，如果和大于目标值，向前移动右指针。
由于一定存在唯一答案，所以左指针一定小于右指针。以此作为循环条件。
```
var twoSum = function(numbers, target) {
    let left = 0, right = numbers.length - 1;
    while(left < right){
        if(numbers[left] + numbers[right] < target){
            left++;
        }else if(numbers[left] + numbers[right] > target){
            right--;
        }else{
            return [left+1, right+1]
        }
    }    
};
```
利用哈希表存贮每个元素及其位置，在通过哈希表搜索能与当前元素组成目标值的元素。但是哈希表查找结果不一定按照大小顺序排列，因此需要对结果进行判断排序。
```
var twoSum = function(numbers, target) {
     let map = new Map();
     let index1 = 0; index2 = 0;
     for(let i = 0; i < numbers.length; i++){
         map.set(numbers[i], i);
         let res = target - numbers[i];
         if(map.has(res)){
             index1 = i;
             index2 = map.get(res);
         }
     }
     if(index1 === index2){
         return [index1, index2+1];
     }else if(index1 < index2){
         return [index1+1, index2+1]
     }else{
         return [index2+1, index1+1]
     }
};
```
