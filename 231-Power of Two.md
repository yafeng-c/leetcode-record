Given an integer, write a function to determine if it is a power of two.


我只想到了笨办法。
```
var isPowerOfTwo = function(n) {
    if(n === 0) return false;
    while(n !== 1){
        if(n % 2 === 0){
            n = Math.floor(n / 2);
        }else{
            return false;
        }
    }
    return true;
};
```
二进制好巧妙。
```
var isPowerOfTwo = function(n) {
    if(n<1){
        return false;
    }

    let m = n & (n-1);
    if(m==0){
        return true;
    }else{
        return false;
    }
};
```
