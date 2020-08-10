```
Given two arrays arr1 and arr2, the elements of arr2 are distinct, and all elements in arr2 are also in arr1.
Sort the elements of arr1 such that the relative ordering of items in arr1 are the same as in arr2.  Elements that don't appear in arr2 should be placed at the end of arr1 in ascending order.

Example 1:
Input: arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
Output: [2,2,2,1,4,3,3,9,6,7,19]
 

Constraints:
arr1.length, arr2.length <= 1000
0 <= arr1[i], arr2[i] <= 1000
Each arr2[i] is distinct.
Each arr2[i] is in arr1.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/relative-sort-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

首先想到了哈希表。
```
var relativeSortArray = function(arr1, arr2) {
    let ans = [];
    let hash = {};
    arr1.sort((a, b) => a-b);
    for(let i = 0; i < arr1.length; i++){
        hash[arr1[i]] ? hash[arr1[i]]++ : hash[arr1[i]] = 1;
    }
    //console.log(typeof(hash[2]))
    for(let j = 0; j < arr2.length; j++){
        while(hash[arr2[j]] != null && hash[arr2[j]] !== 0){
            ans.push(arr2[j]);
            hash[arr2[j]]--;
        }
    }
    for(let i = 0; i < arr1.length; i++){
        if(hash[arr1[i]] !== 0){
            ans.push(arr1[i])
        }
    }
    return ans;
};
```
回顾以前看答案用Java写的代码，不同的是，直接创建数组去记录，就不需要对arr1排序。
```
class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        int l1 = arr1.length;
        int l2 = arr2.length;
        int index = 0;
        int[] result = new int[l1];
        int[] nums = new int[1001];
        for(int i : arr1 ){
            nums[i]++;
        }
        for(int j : arr2){
            while(nums[j] > 0){
                result[index++] = j;
                nums[j]--;
            }
        }
        for(int t = 0; t < 1001; t++){
            while(nums[t] > 0){
                result[index++] = t;
                nums[t]--;
            }
        }
        return result;
    }
}
```
题解里有利用JS的sort直接输出，太强了。
```
var relativeSortArray = function (arr1, arr2) {
            //sort(a,b) 正常a,b中谁小排到前面
            return arr1.sort((a,b)=>{
                let a1 = arr2.indexOf(a);
                let b1 = arr2.indexOf(b);
                if(a1 == -1 && b1 == -1){//如果a和b都不在arr2中，正常的大小升序
                    return a - b;
                }else if(a1 == -1){ //如果a不在arr2中，a-b=1说明a>b，a就得排在后面
                    return 1;
                }else if(b1 == -1){ //如果b不在arr2中，a-b=-1说明b>a，b就得排在后面
                    return -1;
                }else{          //如果都在arr2中，就看他们谁先出现在arr2中，如果a在前面，那么a1就小于b1,return 就是小于0的，所以a在前面
                    return a1-b1;
                }
            })
        };

```
