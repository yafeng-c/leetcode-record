```
Reverse bits of a given 32 bits unsigned integer. 

Example 1:
Input: 00000010100101000001111010011100
Output: 00111001011110000010100101000000
Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.

Example 2:
Input: 11111111111111111111111111111101
Output: 10111111111111111111111111111111
Explanation: The input binary string 11111111111111111111111111111101 represents the unsigned integer 4294967293, so return 3221225471 which its binary representation is 10111111111111111111111111111111.
 

Note:
Note that in some languages such as Java, there is no unsigned integer type. In this case, both input and output will be given as signed integer type and should not affect your implementation, as the internal binary representation of the integer is the same whether it is signed or unsigned.
In Java, the compiler represents the signed integers using 2's complement notation. Therefore, in Example 2 above the input represents the signed integer -3 and the output represents the signed integer -1073741825.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-bits
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
逐位颠倒思路：https://leetcode-cn.com/problems/reverse-bits/solution/li-yong-wei-cao-zuo-jie-ti-qian-xian-yi-dong-by-li/
```
var reverseBits = function(n) {
    let res = 0, i = 31;
    while(i >= 0){
        res += (n&1) << i;
        i--;
        n = n >> 1;
    }
    return res;
};
```
但是JS要考虑有符号的问题，因此在最后的输出要加操作>>> 0。

````
var reverseBits = function(n) {
    let res = 0, i = 31;
    while(i >= 0){
        res += (n&1) << i;
        i--;
        n = n >> 1;
    }
    return res>>>0;
};
````
```
js中表达式 >>> 0 浅析
">>>" 是无符号右移
负数移动n位，总是非负数
">>> 0"意义
将数据转换为number类型
将number转换为无符号的32bit数据
即Uint32类型
如不能转换为Number，则为0
如果为非整数，先转换为整数
parseInt(string,radix)
Math.trunc()
~~n
n | n
n | 0
n << 0
n >> 0
n & n
">>" 是有符号右移
负数移位是负数

作者：Alexer-660
链接：https://leetcode-cn.com/problems/reverse-bits/solution/190-dian-dao-er-jin-zhi-wei-by-alexer-660/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

```
另外一个不需要循环的思路。如果遇到这样的公司，我就挂了吧。
https://leetcode-cn.com/problems/reverse-bits/solution/li-yong-wei-cao-zuo-jie-ti-qian-xian-yi-dong-by-li/
