# Tasks with arrays
+ [Two Sum](#2_sum)
+ [3Sum](#threesome)
+ [Subarray Sum Equals K](#sum_eq)

## Two Sum

https://leetcode.com/problems/two-sum/

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map <int,int> mp;
        for(int i = 0; i < nums.size(); i++){
            map <int,int> :: iterator sum_find = mp.find(target - nums[i]);
            if(sum_find != mp.end())
                return {sum_find->second, i};
            mp.insert(make_pair(nums[i], i));
        }
        return {0};
    }
};
```

## 3sum

https://leetcode.com/problems/3sum/

### Fast

```C++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int size = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int>> result;
        for(int i = 0; i < size - 2; i++){
            if(i > 0 && nums[i - 1] == nums[i])
                continue;
            int left = i + 1;
            int right = size - 1;
            
            while(left < right){
                int sum = nums[i] + nums[left] + nums[right];
                if(!sum)
                    result.push_back({nums[i], nums[left], nums[right]});
                if(sum < 0)
                    while(++left < size && nums[left - 1] == nums[left]);
                else
                    while(--right > 0 && nums[right + 1] == nums[right]);               
            }
        }
        return result;
    }
};
```

### Slow

```C++
class Solution {
public:
    vector<vector<int>> twoSum(vector<int>& nums, int target, int ignoreNum) {
        map <int,int> mp;
        bool k = false;
        vector<vector<int>> result = vector<vector<int>> (0);
        for(int i = ignoreNum + 1; i < nums.size(); i++){
            if(nums[i] == nums[ignoreNum]&& k){
                k = true;
                continue;
            }
            map <int,int> :: iterator it = mp.find(target - nums[i]);
            if(it != mp.end())
                result.push_back({it->first, nums[i], nums[ignoreNum]});
            mp.insert(make_pair(nums[i], i));
        }
        return result;
    }
    bool checkUnique(vector<vector<int>>& result, vector <int> sum){
        for(int i = 0; i < result.size(); i++){
            if(result[i][0] == sum[0] && result[i][1] == sum[1])
                return false;
        }
        return true;
    }
    vector<vector<int>> threeSum(vector<int>& nums) {
        int size = nums.size();
        if(size < 3)
            return {};
        vector<vector<int>> result;
        vector<vector<int>> sum;
        sort(nums.begin(), nums.end());
        for(int i = 0; i < size - 2; i++){
            sum = twoSum(nums, -nums[i], i);
            if(sum != vector<vector<int>> (0)){
                int sumSize = sum.size();
                for(int j = 0; j < sumSize; j++){
                    if(checkUnique(result, sum[j]))
                        result.push_back(sum[j]); 
                }
            }
        }
        return result;
    }
};
```

## Subarray Sum Equals K

https://leetcode.com/problems/subarray-sum-equals-k/

```C++
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        map <int, int> sum_arr;
        int sum = 0;
        int result = 0;
        for(auto elem : nums){
            sum_arr.insert(make_pair(sum, 1));
            sum += elem;
            map <int, int> :: iterator sum_find = sum_arr.find(sum - k);
            if(sum_find != sum_arr.end()){
                result += sum_find->second;
            }
            sum_find = sum_arr.find(sum);
            if(sum_find != sum_arr.end()){
                sum_find->second++;
            }   
        }
        return result;
    }
};
```
