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

```C++
class Solution {
 public:
  int findMin(vector<int>& nums) {
    int left = 0;
    int right = nums.size() - 1;
    if (nums.size() == 1 || nums[right] > nums[0]) return 0;
    while (right >= left) {
      int mid = (right + left) / 2;
      if (nums[mid] > nums[mid + 1]) return mid + 1;
      if (nums[mid - 1] > nums[mid]) return mid;
      if (nums[mid] > nums[0])
        left = mid + 1;
      else
        right = mid - 1;
    }
    return -1;
  }
  int binarySearch(vector<int>& nums, int target, int left, int right) {
    while (right >= left) {
      int mid = (right + left) / 2;
      if (nums[mid] > target) right = mid - 1;
      if (nums[mid] < target) left = mid + 1;
      if (nums[mid] == target) return mid;
    }
    return -1;
  }
  int search(vector<int>& nums, int target) {
    if (nums.size() == 0) return -1;
    int div = findMin(nums);
    return max(binarySearch(nums, target, 0, div - 1),
               binarySearch(nums, target, div, nums.size() - 1));
  }
};
```

## Find Minimum in Rotated Sorted Array

https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/

```C++
class Solution {
 public:
  int findMin(vector<int>& nums) {
    int left = 0;
    int right = nums.size() - 1;
    if (nums.size() == 1 || nums[right] > nums[0]) return nums[0];
    while (right >= left) {
      int mid = (right + left) / 2;
      if (nums[mid] > nums[mid + 1]) return nums[mid + 1];
      if (nums[mid - 1] > nums[mid]) return nums[mid];
      if (nums[mid] > nums[0])
        left = mid + 1;
      else
        right = mid - 1;
    }
    return -1;
  }
};
```
