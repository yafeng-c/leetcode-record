```
Given an array of integers A sorted in non-decreasing order, return an array of the squares of each number, also in sorted non-decreasing order.

 

Example 1:

Input: [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Example 2:

Input: [-7,-3,2,3,11]
Output: [4,9,9,49,121]
 

Note:

1 <= A.length <= 10000
-10000 <= A[i] <= 10000
A is sorted in non-decreasing order.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/squares-of-a-sorted-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

就算第二遍做，当然我只想到了暴力解法，先平方再排序。
利用双指针可以只遍历一次，很巧妙。

```
var sortedSquares = function(A) {
    let ans = new Array(A.length);
    let i = 0, j = A.length - 1, k = A.length - 1;
    while(i <= j){
        if(A[i] + A[j] < 0){
            ans[k--] = A[i] * A[i];
            i++;
        }else{
            ans[k--] = A[j] * A[j];
            j--;
        }
    }
    return ans;  
};
```
