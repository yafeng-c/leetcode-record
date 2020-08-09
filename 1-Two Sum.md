```
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/two-sum
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

除了暴力解法，我首先想到了二分查找提高效率，结果看评论用哈希表更好。
对于只遍历一次的情况，我的代码：
```
var twoSum = function(nums, target) {
    let map = {};
    for(let i = 0; i < nums.length; i++){
        map[nums[i]] = i;
        let reminder = target - nums[i];
        if(map[reminder] != null){
            return [i, map[reminder]]
        }
    }
    return false;    
};
```
这样先赋值再遍历，不能通过nums=[3,2,4]， target=6的情况。正确答案是为[1,2]，而我的答案为[0,0]。
我们知道6=2+4=3+3，由于先赋值了{'3',0}，接下来查找target-nums[i]，即3，会查找到了自己，即刚刚存放的{'3',0}。
一个简单解决思路，增加条件map[reminder] != i。
```
var twoSum = function(nums, target) {
    let map = {};
    for(let i = 0; i < nums.length; i++){
        map[nums[i]] = i;
        let reminder = target - nums[i];
        if(map[reminder] != null && map[reminder] != i){
            return [i, map[reminder]]
        }
    }
    console.log(map)
    return false;    
};
```
但是对于nums=[3,3]， target=6的情况，程序报错。
因为map的键值设定为nums中每个元素的值，遍历nums的第二个3时，会覆盖掉原先的值。即{'3',0}变成了{'3',1}。
对比其他人的题解发现，通过先遍历查询再赋值可以避免上述的问题。
```
var twoSum = function(nums, target) {
    let map = {};
    for(let i = 0; i < nums.length; i++){
        let reminder = target - nums[i];
        if(map[reminder] != null){
            return [i, map[reminder]]
        }
        map[nums[i]] = i;
    }
    return false;    
};
```
遍历到第二个3时，由于还未覆盖掉原先的{'3',0}，因此查找target-nums[i]仍然能找到第一个3。同时也避免了查找到自己的情况。
