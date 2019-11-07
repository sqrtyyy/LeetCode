# Binary Search
+ [Binary Search](#binary-search)
+ [Search in Rotated Sorted Array](#search-in-rotated-sorted-array)
+ [Find Minimum in Rotated Sorted Array](#find-minimum-in-rotated-sorted-array)

## Binary Search

https://leetcode.com/problems/binary-search/

```C++
class Solution {
 public:
  int search(vector<int>& nums, int target) {
    int left = 0;
    int right = nums.size() - 1;
    while (right - left > 1) {
      int mid = (right + left) / 2;
      if (nums[mid] > target) right = mid;
      if (nums[mid] < target) left = mid;
      if (nums[mid] == target) return mid;
    }
    return nums[left] == target ? left : nums[right] == target ? right : -1;
  }
};
```

## Search in Rotated Sorted Array

https://leetcode.com/problems/search-in-rotated-sorted-array/

## Find Minimum in Rotated Sorted Array

https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/
