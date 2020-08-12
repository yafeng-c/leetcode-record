```
Given a non-empty array of non-negative integers nums, the degree of this array is defined as the maximum frequency of any one of its elements.
Your task is to find the smallest possible length of a (contiguous) subarray of nums, that has the same degree as nums. 

Example 1:
Input: nums = [1,2,2,3,1]
Output: 2
Explanation: 
The input array has a degree of 2 because both elements 1 and 2 appear twice.
Of the subarrays that have the same degree:
[1, 2, 2, 3, 1], [1, 2, 2, 3], [2, 2, 3, 1], [1, 2, 2], [2, 2, 3], [2, 2]
The shortest length is 2. So return 2.

Example 2:
Input: nums = [1,2,2,3,1,4,2]
Output: 6
Explanation: 
The degree is 3 because the element 2 is repeated 3 times.
So [2,2,3,1,4,2] is the shortest subarray, therefore returning 6.
 

Constraints:
nums.length will be between 1 and 50,000.
nums[i] will be an integer between 0 and 49,999.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/degree-of-an-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
建立哈希表统计每个元素出现次数，进而确定度。
再遍历数组，创建另一个表，找出使得在新表出现次数和度相同的元素在数组中首次出现的位置（indexOf返回参数首次出现位置）。
比如[1,2,2,3,1]，度为2，使得度为2的元素有1和2。元素1在新表出现次数和度相同的位置是4，其首次出现的位置是0。元素2在新表出现次数和度相同的位置是2，其首次出现的位置是1。
```
var findShortestSubArray = function(nums) {
    let degreeMap = new Map(), size = 1, distance = nums.length;
    for(let num of nums){
        degreeMap.set(num, degreeMap.has(num) ? degreeMap.get(num) + 1 : 1);
        size = Math.max(size, degreeMap.get(num))
    }
    let helpMap = new Map();
    for(let i = 0; i < nums.length; i++){
        helpMap.set(nums[i], helpMap.has(nums[i]) ? helpMap.get(nums[i]) + 1 : 1)
        if(helpMap.get(nums[i]) === size){
            let start = nums.indexOf(nums[i]);
            distance = Math.min(distance, i - start + 1);
        }
    }
    return distance;
};
```
还可以通过用一个左位置表和右位置表记录每个元素首次和最后一次出现的位置。
```
var findShortestSubArray = function(nums) {
    let left = new Map(), right = new Map(), count = new Map();
    let degree = 1, distance = nums.length;
    for(let i = 0; i < nums.length; i++){
        let num = nums[i];
        if(!left.has(num)){
            left.set(num, i)
        }
        right.set(num, i);
        count.set(num, count.has(num) ? count.get(num) + 1 : 1);
        degree = Math.max(degree, count.get(num));
    }
    for(let x of count.keys()){
        if(count.get(x) === degree){
            distance = Math.min(distance, right.get(x) - left.get(x) + 1);
        }
    }
    return distance;
};
```
方法二的思路曾经用Java写过，运行时间10ms比JS的104ms快很多。
```
class Solution {
    public int findShortestSubArray(int[] nums) {
        int[] counts = new int[50000];
        for (int num : nums) {
            counts[num] ++;
        }
        //key为元素，value为其度值
        int key = -1, value = -1;
        //找到度最大的元素是哪个
        for (int i = 0; i < counts.length; i ++) {
            if (counts[i] > value) {
                key = i;
                value = counts[i];
            }
        }
        Map<Integer, Integer> left = new HashMap<>();
        Map<Integer, Integer> right = new HashMap<>();

        for (int i = 0; i < nums.length; i ++) {
            if (counts[nums[i]] == value) {
                if (!left.containsKey(nums[i])) {
                    left.put(nums[i], i);
                }
            }
        }
        for (int i = nums.length - 1; i >= 0; i --) {
            if (counts[nums[i]] == value) {
                if (!right.containsKey(nums[i])) {
                    right.put(nums[i], i);
                }
            }
        }
        //此时left和right分别保存了数量重复最多的元素，他们的左右界限情况
        int res = Integer.MAX_VALUE;
        for (Map.Entry<Integer, Integer> entry : left.entrySet()) {
            res = Math.min(res, right.get(entry.getKey()) - entry.getValue() + 1);
        }
        return res;
    }
}
```
