# LeetCode Notebook
Hairong's LeetCode Notebook🟢🟡🔴

## Topics
- **[Array](#array)**
- **String**

## Arrays <a id="array"></a>
| Problem | Solution | Difficulty |
|-----------------|-----------------|-----------------|
| [3Sum](https://leetcode.com/problems/3sum/description/) | [Solution](#15) | 🟡 Medium |
| Row 2 Column 1 | Row 2 Column 2 | Row 2 Column 3 |
| Row 3 Column 1 | Row 3 Column 2 | Row 3 Column 3 |

___
### 3Sum <a id="15"></a>
follow the same two pointers pattern as in [TwoSumII](https://www.notion.so/167-Two-Sum-II-Input-Array-Is-Sorted-1655664799b84966a2fded885443670f).

To make sure the result contains unique triplets, we need to **skip duplicate values**. It is easy to do because repeating values are next to each other in a sorted array.

> 💡 **2 Pointers**
```python
class Solution(object):
    def threeSum(self, nums):

        res = []
        nums.sort()

        for i in range(len(nums)):
            if nums[i] > 0: # since we sorted the array, if current value > 0, the rest cannot sum up to 0
                break
            if i == 0 or nums[i] != nums[i - 1]: # if the current value == last value, there's duplicate, skip it
                self.twoSumII(nums, i, res)
        return res

    def twoSumII(self, nums, i, res):
        lo = i + 1
        hi = len(nums) - 1

        while lo < hi:
            sum = nums[i] + nums[lo] + nums[hi]
            if sum < 0:
                lo += 1
            elif sum > 0:
                hi -= 1
            else:
                res.append([nums[i], nums[lo], nums[hi]])
                lo += 1
                hi -= 1
                while lo < hi and nums[lo] == nums[lo - 1]: # if the next value is same as before, skip it
                    lo += 1
```

> 💡 **No Sort**

in case we cannot modify the input array
use hashset approach to work for unsorted array.
[Solution link](https://leetcode.com/problems/3sum/editorial/)
```python
class Solution(object):
    def threeSum(self, nums):

        res = set() # avoid duplicate in result
        dups = set() # avoid duplicate in each iteration

        for i, val1 in enumerate(nums):
            seen = set() # to put all the value we have seen before

            if val1 not in dups: # skip duplicate in outer loop
                dups.add(val1)

                for j, val2 in enumerate(nums[i + 1:]): # inner loop
                    complement = - val1 - val2  # get the complement, since we want val1 + val2 + complement = 0

                    if complement in seen: # if we seen the complement before we found a three sum
                        res.add(tuple(sorted((val1, val2, complement)))) # add values in sorted way so that we can remove dup easily
                    seen.add(val2) # otherwise we put value we have seen in the inner loop

        return res
```
---
