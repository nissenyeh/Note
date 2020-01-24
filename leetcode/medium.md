

### 3. split-a-string-in-balanced-strings
```py
import random

class Solution:
    def sortArray(self, nums):

        if len(nums) <= 1:
            return nums
        
        ran = random.choice(nums)
        print(ran)

        small = [v for v in nums if v < ran]
        equal = [v for v in nums if v == ran]
        larger = [v for v in nums if v > ran]
        
        return self.sortArray(small) + equal + self.sortArray(larger)
        

obj = Solution()
print(obj.sortArray([1,2,3,10,2,4]))
```