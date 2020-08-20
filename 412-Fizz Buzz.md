```
Write a program that outputs the string representation of numbers from 1 to n.
But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

Example:
n = 15,
Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/fizz-buzz
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```
当然我只想到了暴力法。
```
var fizzBuzz = function(n) {
    let res = [];
    for(let i = 1; i <= n; i++){
        if(i%3 !== 0 && i%5 !== 0){
            res.push(i.toString())
        }else if(i%3 === 0 && i%5 !== 0){
            res.push('Fizz')
        }
        else if(i%3 !== 0 && i%5 == 0){
            res.push('Buzz')
        }else if(i%3 === 0 && i%5 === 0){
            res.push('FizzBuzz')
        }
    }
    return res;
};
```
把映射关系放到hash表中，非常优雅。
```
var fizzBuzz = function(n) {
    let res = [];
    let map = new Map();
    map.set(3,'Fizz');
    map.set(5,'Buzz');
    for(let i = 1; i <= n; i++){
        let temp = '';
        for(let key of map.keys()){
            if(i%key === 0){
                temp += map.get(key)
            }
        }
        if(temp === ''){
            temp = i.toString();
        }
        res.push(temp)
    }
    return res;
};
```
