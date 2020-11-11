```
Given the array nums consisting of 2n elements in the form [x1,x2,...,xn,y1,y2,...,yn].

Return the array in the form [x1,y1,x2,y2,...,xn,yn].

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/shuffle-the-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```

```
class Solution:
    def shuffle(self, nums: List[int], n: int) -> List[int]:
        for i in range(0, 2*n):
            if nums[i] > 0:
                j = i
                while(nums[i] > 0):
                    if j < n: j = 2*j
                    else: j = 2*(j-n)+1
                    nums[i],nums[j]=nums[j],-nums[i]
        for i in range(0, 2*n):
            nums[i] = -nums[i]
        return nums
```
detailed execution of the swap process
```
[x1(+),x2(+),x3(+),y1(+),y2(+),y3(+)]
i = 0, nums[i]=nums[0]=x1>0,
j = i = 0,
while nums[i]=x1>0
j = 0 < n = 3,
j = 2*i=2*0=0
nums[0],nums[0]=nums[0],-nums[0] => swap x1 and x1
[x1(-),x2(+),x3(+),y1(+),y2(+),y3(+)]
nums[0]=-x1<0 break while
i = 1, nums[1]=x2>0,
j = 1
while nums[i]=x2>0
j = 1 < n = 3,
j = 2*j = 2,
nums[1],nums[2]=nums[2],-nums[1] => swap x2 with x3,
nums[1] = x3, nums[2] = -x2
[x1(-),x3(+),x2(-),y1(+),y2(+),y3(+)]
still while nums[1]=x3>0,
j = 2 < 3, j = 2*2 = 4,
nums[1],nums[4]=nums[4],-nums[1] => swap x3 with y2,
nums[1] = y2, nums[4] = -x3
[x1(-),y2(+),x2(-),y1(+),x3(-),y3(+)]
still while nums[1]=y2>0,
j = 4 > 3, j = 2*(4-1)+1=3,
nums[1],nums[3]=nums[3],-nums[1] => swap y2 with y1,
nums[1] = y1, nums[3] = -y2,
[x1(-),y1(+),x2(-),y2(-),x3(-),y3(+)]
still while nums[1]=y1>0,
j = 3 = 3, j = 2*(3-3)+1=1,
nums[1],nums[1]=nums[1],-nums[1] => swap y1 with itself,
nums[1]=-y1,
break the while
[x1(-),y1(-),x2(-),y2(-),x3(-),y3(+)]
continue the for i in range(0,2*n),
when i = 1, nums[1]<0,...
when i = 5, nums[1]>0,
j = i = 5,
while nums[5]>0,
j = 5 > 3, j = 2*(5-3)+1 = 5,
so swap nums[5] with itself,
nums[5]=-y3,
[x1(-),y1(-),x2(-),y2(-),x3(-),y3(-)]
break the while and end the for loop
```
