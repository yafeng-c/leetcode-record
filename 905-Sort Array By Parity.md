```
Given an array A of non-negative integers, return an array consisting of all the even elements of A, followed by all the odd elements of A.
You may return any answer array that satisfies this condition. 

Example 1:
Input: [3,1,2,4]
Output: [2,4,3,1]
The outputs [4,2,3,1], [2,4,1,3], and [4,2,1,3] would also be accepted. 

Note:
1 <= A.length <= 5000
0 <= A[i] <= 5000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/sort-array-by-parity
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
一遍一次，同时将奇数和偶数存储到不同数组，最后合并两个数组。
```
let oddEle = [], evenEle = [];
    for(let i = 0; i < A.length; i++){
        if(A[i] % 2 === 0){
            evenEle.push(A[i])
        }else{
            oddEle.push(A[i])
        }
    }
    return evenEle.concat(oddEle);
```
通过维护两个指针实现原地修改。
```
var sortArrayByParity = function(A) {
    let i = 0, j = A.length - 1;
    while(i < j){
        if(A[i] % 2 === 0 && A[j] % 2 === 1){
            i++;
            j--;
        }else if(A[i] % 2 === 0 && A[j] % 2 !== 1){
            i++;
        }else if(A[i] % 2 !== 0 && A[j] % 2 === 1){
            j--;
        }else{
            let temp = A[i];
            A[i] = A[j];
            A[j] = temp;
        }
    }
    return A;
};
```
