```
Given a 32-bit signed integer, reverse digits of an integer.

Example 1:

Input: 123
Output: 321

Example 2:

Input: -123
Output: -321

Example 3:

Input: 120
Output: 21

Note:

Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-integer
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

这段代码没有考虑溢出的情况，而且当输入为负数时，会进入死循环，因为Math.floor()会向下取整。
```
var reverse = function(x) {
    let ans = 0;
    while(x != 0){
        num = x%10;
        ans = ans*10 + num;
        x = Math.floor(x/10)
    }
    return ans;
};
```
通过按位与实现正数向下取整，负数向上取整。
```
var reverse = function(x) {
    let ans = 0;
    while(x != 0){
        ans = ans*10 + x%10;
        x = (x/10) | 0; /*通过按位与取整*/
    }
    return ((ans | 0) === ans) ? ans : 0; /*考虑溢出*/
};
```

按位与操作参考：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_Operators

