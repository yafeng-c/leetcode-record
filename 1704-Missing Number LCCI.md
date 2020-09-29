```
An array contains all the integers from 0 to n, except for one number which is missing.  Write code to find the missing integer. Can you do it in O(n) time?

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/missing-number-lcci
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```
var missingNumber = function(nums) {
    let res = 0;
    for(let i = 0; i < nums.length; i++){
        res = res ^ i;
        res = res ^ nums[i];
    }
    return res ^ nums.length;    
};
```

0和任何值的异或等于本身，即 A ^ 0 = A

异或本身等于0，即 A ^ A = 0

异或满足结合律，即 A ^ B ^ C = A ^ ( B ^ C)
