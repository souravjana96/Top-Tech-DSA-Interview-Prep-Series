## Leetcode 1095 Solution

### Python

```python
class Solution:
    def find_peak(self, arr, l, h):
        while l < h:
            m = l + (h-l)//2
            if arr.get(m) < arr.get(m+1):
                l = m+1
            else:
                h = m

        return l

    def binary_search_for_increasing_order_part(self, arr, l, h, target):
        while l <= h:
            m = l + (h-l)//2
            if arr.get(m) == target:
                return m
            elif arr.get(m) < target:
                l = m+1
            else:
                h = m-1
        return -1

    def binary_search_for_decreasing_order_part(self, arr, l, h, target):
        while l <= h:
            m = l + (h-l)//2
            if arr.get(m) == target:
                return m
            elif arr.get(m) < target:
                h = m-1
            else:
                l = m+1
        return -1

    def findInMountainArray(self, target: int, mountain_arr: 'MountainArray') -> int:
        n = mountain_arr.length()

        peak_ele_index = self.find_peak(mountain_arr, 0, n-1)
        inc_index  = self.binary_search_for_increasing_order_part(mountain_arr, 0, peak_ele_index, target)

        if inc_index != -1:
            return inc_index

        dec_index = self.binary_search_for_decreasing_order_part(mountain_arr, peak_ele_index+1, n-1, target)
        return dec_index
```
