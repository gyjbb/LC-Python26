# LC-Python26
Greedy Algorithm 1

## Theory, 455.Assign Cookies, 376.Wiggle Subsequence, 53.Maximum Subarray

June 26, 2023  4h

Congratulations!\
This is the 26th day for leetcode python study. Today we will learn about the Greedy Algorithm!\
The challenges today are about ~~need to delete later~~.


## Theory
The greedy theory has no law. Later we will learn its difference with dynamic programming。


## 455.Assign Cookies
Here we always use the larger cookies to feed the older kids.\
The second loop needs a constraint to control the loop, so we use while rather than for. The outer for loop gradually decreases no matter what happens, the inner while loop will only adjust the indexes when the constraint condition is met.
```python
# ways 1: 
class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        g.sort()
        s.sort()
        index = len(s)-1    #start with the largest cookie
        result = 0      #to record the match
        for i in range(len(g)-1, -1, -1):
            if index >= 0 and s[index] >= g[i]:
                result += 1
                index -= 1
        return result
```


## 376.Wiggle Subsequence
Keep the peaks and remove the numbers on the slope. The solution will only record the peak ups and downs, and emit those on the slope.\
There are two special conditions here, one is the steady slope, we include this situation by prediff>=0 and curdiff<0 or prediff<=0 and curdiff>0. \
The other special situation is that the array only has 2 numbers and the result should be 2. We could add a dummy head with number same as the first number, and set the result default start from 1, and for loop end until the second last number.\
When there is a wiggle, we update the prediff with the current diff value. If no wiggle, the prediff remains the same.
```python
class Solution:
    def wiggleMaxLength(self, nums: List[int]) -> int:
        if len(nums) <= 1:
            return len(nums)
        
        curDiff = 0
        preDiff = 0
        result = 1      #set default start from 1
        for i in range(len(nums)-1):     #loop until the second last number
            curDiff = nums[i+1] - nums[i]
            # when we meet a wiggle
            if (preDiff <= 0 and curDiff > 0) or (preDiff >= 0 and curDiff < 0):
                result += 1     #record this wiggle
                preDiff = curDiff      #update prediff only when there is a new wiggle, for recording purpose like two pointers
        return result
```


## 53.Maximum Subarray
最大子序和  
