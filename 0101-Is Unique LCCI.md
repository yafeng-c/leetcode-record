```
Implement an algorithm to determine if a string has all unique characters. What if you cannot use additional data structures?

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/is-unique-lcci
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

用位运算保存访问过的元素。

```
var isUnique = function(astr) {
    let mark = 0;
    for(let char of astr){
        let move = char.charCodeAt() - 97;
        if((mark & (1 << move)) !== 0){
            return false;
        }
        mark = mark | (1 << move)        
    }
    return true;
};
```
