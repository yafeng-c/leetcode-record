```
We have n chips, where the position of the ith chip is position[i].

We need to move all the chips to the same position, In one step, we can change the position of the ith chip from position[i] to:

position[i] + 2 or position[i] - 2 with cost = 0.
position[i] + 1 or position[i] - 1 with cost = 1.
Return the minimum cost needed to move all the chips to the same position.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/minimum-cost-to-move-chips-to-the-same-position
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```
分别统计奇数位置和偶数位置的个数，相当于把所有奇数放一起，所有偶数的放一起，然后比较奇数的少还是偶数的少，将少的个数移到多的个数位置上去就可以了.

作者：Athenahe126
链接：https://leetcode-cn.com/problems/minimum-cost-to-move-chips-to-the-same-position/solution/xian-li-jie-ti-yi-zai-li-jie-dai-ma-si-lu-by-athen/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

让我想起了小学时代被奥数支配的恐惧。

```
var minCostToMoveChips = function(position) {
    let odd = 0, even = 0;
    for(let i = 0; i < position.length; i++){
        if(position[i] % 2 === 0){
            even++;
        }else{
            odd++;
        }
    }
    return Math.min(odd, even)
};
```
