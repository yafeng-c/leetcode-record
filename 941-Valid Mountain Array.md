```
Given an array A of integers, return true if and only if it is a valid mountain array.
Recall that A is a mountain array if and only if:

A.length >= 3
There exists some i with 0 < i < A.length - 1 such that:
A[0] < A[1] < ... A[i-1] < A[i]
A[i] > A[i+1] > ... > A[A.length - 1]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/valid-mountain-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

其实用暴力法效果还可以。（运行时间88 ms，内存消耗40.6 MB）
```
var validMountainArray = function(A) {
    if(A.length < 3) return false;
    if(A[0] > A[1]) return false;
    let i = 1;
    while(i < A.length - 1){
        if(A[i] <= A[i-1]){
            break;
        }
        i++;
    }
    let j = i-1;
    while(j < A.length){
        if(A[j] <= A[j+1]){
            return false;
        }
        j++;
    }
    return true;
};
```

评论有提到双指针，我也想到过，但没写。需要注意的是两个指针开始和结束的位置。
（运行时间104 ms 内存消耗40.3 MB）
```
 var validMountainArray = function(A) {
    if(A.length < 3) return false;
    let left = 0, right = A.length - 1;
    while(left < A.length - 2 && A[left] < A[left+1]){
        left++;
    }
    while(right > 1 && A[right] < A[right-1]){
        right--;
    }
    return left === right
};
```
