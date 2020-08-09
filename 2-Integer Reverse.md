Given a 32-bit signed integer, reverse digits of an integer.

>

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
