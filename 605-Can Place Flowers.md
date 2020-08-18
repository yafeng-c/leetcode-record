```
Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.
Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number n, return if n new flowers can be planted in it without violating the no-adjacent-flowers rule.

Example 1:
Input: flowerbed = [1,0,0,0,1], n = 1
Output: True

Example 2:
Input: flowerbed = [1,0,0,0,1], n = 2
Output: False

Note:
The input array won't violate no-adjacent-flowers rule.
The input array size is in the range of [1, 20000].
n is a non-negative integer which won't exceed the input array size.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/can-place-flowers
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
这种首位默认有0，末尾补0的方法我真的打死都想不到。
```
var canPlaceFlowers = function(flowerbed, n) {
    flowerbed.push(0);
    let cnt = 0, total = 1;
    for(let i = 0; i < flowerbed.length; i++){
        if(flowerbed[i] === 0){
            total++;
            if(total === 3){
                cnt++;
            }
        }else{
            total = 0;
        }
    }
    return cnt <= n;
};
```
