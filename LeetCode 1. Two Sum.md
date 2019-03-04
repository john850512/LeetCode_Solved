# LeetCode 1. Two Sum
- https://leetcode.com/problems/two-sum
#### Approach 1: Brute Force
分析:
- Time Complexity: O(N^2)
- Space Complexity: O(1)


``` c
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ans;
        for(int i = 0 ; i < nums.size() ; i++){
            for(int j = i+1; j < nums.size(); j++){
                if(nums[i] + nums[j] == target){
                    ans = {i,j};
                    return ans;
                }
            }
        }
        return ans;
    }
};
```

#### Approach 2: Two-pass Hash Table
在上面中，查詢target-nums[k]是否存在需要花費O(N)的時間

透過hash table可以在近似O(1)的時間做到value和index的查詢(如果collision發生則可能到O(N))

簡單的做法就是先建表(O(N))，然後只要給定nums[i]，查詢是否有target-nums[i]存在即可(O(N))

在STL中:
- 建構map預設是使用[紅黑樹](https://www.youtube.com/watch?v=-GAGKRDRP1M)，查詢的時間複雜度是O(logN)
- unordered_map使用的是hash_table，查詢的時間複雜度是O(1)，但會花費相對多的空間複雜度

分析:
- Time Complexity: O(N)
- Space Complexity: O(N)
  - hash table建構需要N個空間   

``` c
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int, int> hash_table;
        vector<int> ans;
        for(int i = 0 ; i < nums.size() ; i++){
            hash_table.insert(pair<int, int>(nums[i], i));
        }
        for(int i = 0 ; i < nums.size() ; i++){
            int complement = target - nums[i];
            map<int, int>::iterator iter = hash_table.find(complement);
            // printf("%d %d\n", i, iter->second);
            if(iter != hash_table.end() && iter->second != i){
                ans = {i, iter->second};
                return ans;
            }
        }
        return ans;
    }
};
```

#### Approach 3: One way
一邊建表一邊查詢，如果當下有符合的(題目假設一定有符合的)就直接回傳。
