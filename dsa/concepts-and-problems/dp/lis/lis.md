# Longest Increasing Subsequence

```cpp
class Solution {
public:
    int f(int ind,int prevInd,vector<int>& nums,vector<vector<int>>& dp ){
        if(ind==nums.size()) return 0;
        if(dp[ind][prevInd+1]!=-1) return dp[ind][prevInd+1];
        int take=0;
        int notTake=0;
        if(prevInd==-1 || nums[ind]>nums[prevInd])
            take=1+f(ind+1,ind,nums,dp);
        notTake=f(ind+1,prevInd,nums,dp);

        return dp[ind][prevInd+1]=max(take,notTake);
    }
    int lengthOfLIS(vector<int>& nums) {
        int n=nums.size();
        // vector<vector<int>> dp(n,vector<int>(n+1,-1));
        // return f(0,-1,nums,dp);

        // vector<vector<int>> dp(n+1,vector<int>(n+1,0));
        // for(int ind=n-1;ind>=0;ind--){
        //     for(int prevInd=ind-1;prevInd>=-1;prevInd--){
        //         int take=0;
        //         int notTake=0;
        //         if(prevInd==-1 || nums[ind]>nums[prevInd])
        //             take=1+dp[ind+1][ind+1];
        //         notTake=dp[ind+1][prevInd+1];

        //         dp[ind][prevInd+1]=max(take,notTake);
        //     }
        // }
        // return dp[0][0];

        // vector<int> next(n+1,0);
        // vector<int> cur(n+1,0);
        // for(int ind=n-1;ind>=0;ind--){
        //     for(int prevInd=ind-1;prevInd>=-1;prevInd--){
        //         int take=0;
        //         int notTake=0;
        //         if(prevInd==-1 || nums[ind]>nums[prevInd])
        //             take=1+next[ind+1];
        //         notTake=next[prevInd+1];

        //         cur[prevInd+1]=max(take,notTake);
        //     }
        //     next=cur;
        // }
        // return next[0];

        // vector<int> dp(n,1); // the length of the LIS that ends at index i;
        // int maxi=0;
        // for(int i=0;i<n;i++){
        //     for(int prev=0;prev<i;prev++){
        //         if(nums[prev] < nums[i] && 1+dp[prev] > dp[i]){
        //             dp[i]= 1+dp[prev];
        //         }
        //     }
        //     maxi=max(maxi,dp[i]);
        // }
        // return maxi;

        // LIS using Binary Search
        vector<int> temp;
        temp.push_back(nums[0]);
        for(int i =1;i<n;i++){
            if(nums[i]> temp.back()){
                temp.push_back(nums[i]);
            }
            else{
                int ind = lower_bound(temp.begin() ,temp.end() , nums[i])-temp.begin(); // find the index of the smallest element in temp that is (just) greater than or equal to nums[i]
                temp[ind]=nums[i];
            }
        }
        return temp.size();
    }
    
};
```

## Approach 1: Recursion + Memoization
- Time Complexity: O(n^2) - We are solving a subproblem for each combination of `ind` and `prevInd`, where `ind` can take n values and `prevInd` can also take n values (including -1). Therefore, the total number of subproblems is O(n^2).
- Space Complexity: O(n^2) - We are using a 2D dp array of size n x (n+1) to store the results of subproblems, which requires O(n^2) space. Additionally, the recursion stack can go up to O(n) in the worst case, but the dominant factor is the dp array.

## Approach 2: Tabulation
- Time Complexity: O(n^2) - We are filling a 2D dp array of size n x (n+1), which requires O(n^2) time.
- Space Complexity: O(n^2) - We are using a 2D dp array of size n x (n+1) to store the results of subproblems, which requires O(n^2) space.

## Approach 3: Space Optimization
- Time Complexity: O(n^2) - We are filling two 1D arrays of size n+1, which requires O(n^2) time.
- Space Complexity: O(n) - We are using two 1D arrays of size n+1 to store the results of subproblems, which requires O(n) space.

## Approach 4: Dynamic Programming (LIS using dp[])
- Time Complexity: O(n^2) - We are filling a dp array of size n, and for each element, we are checking all previous elements to find the length of the longest increasing subsequence that ends at that element. This results in O(n^2) time complexity.
- Space Complexity: O(n) - We are using a dp array of size n to store the length of the longest increasing subsequence that ends at each index, which requires O(n) space.

## Approach 5: Binary Search - Patience Sorting
- Time Complexity: O(n log n) - We are iterating through the array of length n once, and for each element, we are performing a binary search on the `temp` array, which can have at most n elements. The binary search operation takes O(log n) time, resulting in a total time complexity of O(n log n).
- Space Complexity: O(n) - In the worst case, the `temp` array can grow to the size of n if all elements in the input array are in increasing order. Therefore, the space complexity is O(n).