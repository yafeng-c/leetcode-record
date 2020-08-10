```
You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.
Given n, find the total number of full staircase rows that can be formed.
n is a non-negative integer and fits within the range of a 32-bit signed integer.

Example 1:
n = 5
The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.
Example 2:
n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/arranging-coins
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

其实这个题利用等差数列的特性可以快速求解。看评论提到了二分查找，觉得很有意思。因为这个题没有一个明确的target做比较。

二分查找的两个开始点(left, right)选取也很重要，利用数值n所能组成的梯度行数不会超过n，可以将n考虑作为右边起始点。
```
var arrangeCoins = function(n) {
    if(n === 0) return 0;
    let low = 0, high = n;
    while(low <= high){
        let mid = Math.floor((low+high)/2);
        let sum = mid*(mid+1)/2;
        if(sum > n){
            high = mid - 1;
        }else{
            low = mid + 1;
        }
    }
    return high;
};
```

不过二分查找的边界情况特别麻烦，不知道有什么规律。
right应该取n还是n-1，mid应该向下取整还是向上取整，每次更新左右指针，取值mid还是mid+(-)1，最后返回left还是right。
每个地方都会对结果产生很大的影响，想不出有什么规律，只有套几个值去试。
