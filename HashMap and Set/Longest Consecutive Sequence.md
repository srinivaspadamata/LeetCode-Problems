Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.  
You must write an algorithm that runs in O(n) time.  
  
Example 1:  
Input: nums = [100,4,200,1,3,2]  
Output: 4  
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.  
  
Example 2:  
Input: nums = [0,3,7,2,5,8,4,6,0,1]  
Output: 9  
  
Example 3:  
Input: nums = [1,0,1,2]  
Output: 3  
  
Constraints:  
0 <= nums.length <= 105  
-109 <= nums[i] <= 109  
  
Code: Java  
  
**Optimized:**  
Time Complexity: O(n)  
Space Complexity: O(n), For storing numbers in the HashSet.  
  
```
class Solution {
    public int longestConsecutive(int[] nums) {
        int n = nums.length;
        HashSet<Integer> set = new HashSet<>();
        int longest = 0;

        for(int i=0; i<n; i++) set.add(nums[i]);

        for(int num: set){
            if(!set.contains(num-1)){
                int current = num;
                int streak = 1;

                while(set.contains(current + 1)){
                    current++;
                    streak++;
                }

                longest = Math.max(longest, streak);
            }
        }
        return longest;
    }
}
```
  
**Brute Force:**  
Time Complexity: O(n logn), for sorting  
Space Complexity: O(1)  
  
```
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length == 0) return 0;

        Arrays.sort(nums);
        int longest = 1, current = 1;

        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) continue; // skip duplicates
            if (nums[i] == nums[i - 1] + 1) current++;
            else {
                longest = Math.max(longest, current);
                current = 1;
            }
        }
        return Math.max(longest, current);
    }
}
```
