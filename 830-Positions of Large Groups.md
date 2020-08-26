```
In a string S of lowercase letters, these letters form consecutive groups of the same character.
For example, a string like S = "abbxxxxzyy" has the groups "a", "bb", "xxxx", "z" and "yy".
Call a group large if it has 3 or more characters.  We would like the starting and ending positions of every large group.
The final answer should be in lexicographic order.

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/positions-of-large-groups
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
维护一个start指针。
```
var largeGroupPositions = function(S) {
    if(S.length < 3) return [];
    let start = 0;
    let res = [];
    for(let i = 1; i < S.length;){
        let count = 1;
        let temp = [];
        while(S[start] === S[i]){
            count++;
            if(count === 3){
                temp.push(start)
            }
            i++;
        }
        if(count >= 3){
            temp.push(start + count - 1);
            res.push(temp);
        } 
        start = i;
        i++;
    }
    return res;
};
```
本来也想维护一个start和end指针来着，但是没想好怎么改变i和end。
```
var largeGroupPositions = function (s) {
  if (s.length < 3) {
    return [];
  }
  let start = 0;
  let end = 0;
  let count = 1;
  let res = [];
  for (let i = 1; i < s.length; i++) {
    if (s[i] === s[i - 1]) {
      count++;
      end = i
    } else {
      if (count > 2) {
        res.push([start, end]);
      }
      count = 1;
      start = i;
    }
  }
  if (count > 2) {
    res.push([start, end]);
  }
  return res;
};

作者：linjiajian999
链接：https://leetcode-cn.com/problems/positions-of-large-groups/solution/js-jie-ti-shi-jian-100nei-cun-9762-by-linjiajian99/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```
