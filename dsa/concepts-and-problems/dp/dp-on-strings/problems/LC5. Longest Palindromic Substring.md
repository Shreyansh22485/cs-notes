# LC5. Longest Palindromic Substring

[LeetCode Problem Link](https://leetcode.com/problems/longest-palindromic-substring/)

## Intuition & Approach
The goal is to find the longest palindromic substring in a given string $s$. We can solve this problem using two different approaches.

### Approach 1: Dynamic Programming (Bottom-Up)
- We define a 2D boolean array `dp[i][j]` which is `true` if the substring `s[i...j]` is a palindrome.
- We iterate over all possible substring lengths $L$ from 1 to $N$:
  - **Length 1** ($i == j$): Any single character is a palindrome: `dp[i][j] = true`.
  - **Length 2** ($i + 1 == j$): The substring is a palindrome if the two characters are equal: `dp[i][j] = (s[i] == s[j])`.
  - **Length > 2**: The substring is a palindrome if the boundary characters match ($s[i] == s[j]$) and the inner substring is also a palindrome: `dp[i][j] = (s[i] == s[j] && dp[i+1][j-1])`.
- If `dp[i][j]` is `true` and the current length $L$ is greater than `maxLength`, we update `maxLength = L` and record the starting index `start = i`.
- Finally, return `s.substr(start, maxLength)`.

### Approach 2: Expand Around Center (Two Pointers)
- A palindrome is symmetric about its center. There are $2N - 1$ potential centers in a string of length $N$:
  - $N$ single-character centers (odd-length palindromes).
  - $N - 1$ gap centers between adjacent characters (even-length palindromes).
- For each center, we expand outward using two pointers (`left` moving left, `right` moving right) as long as `s[left] == s[right]`.
- The helper function returns the matching substring. We track and return the longest substring found across all expansions. This avoids the $O(N^2)$ memory table.

## Code Implementation

### Approach 1: Dynamic Programming (Bottom-Up)
```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        int n = s.size();

        vector<vector<int>> dp(n,vector<int>(n,false));

        int maxLength = 1;
        int start = 0;
        int end = 0;

        for(int L=1;L<=n;L++){
            for(int i=0;i+L-1 < n;i++){
                int j = i + L - 1;

                if(i==j){
                    dp[i][j] = true;
                }
                else if(i+1 ==j){
                    dp[i][j] = (s[i] == s[j]);
                }
                else{
                    dp[i][j] = ((s[i] == s[j]) && dp[i+1][j-1]);
                }

                if(dp[i][j] == true && L > maxLength){
                    maxLength = L ;
                    start = i;
                    end = j;
                }
            }
        }
        return s.substr(start,maxLength);
    }
};
```

### Approach 2: Expand Around Center (Two Pointers)
```cpp
class Solution {
public:
    string expand(string s, int left, int right){
        int n=s.size();

        while(left>=0 && right<n && s[left]==s[right]){
            left--;
            right++;
        }
        return s.substr(left+1,right-left-1);
    }
    string longestPalindrome(string s) {
        int n=s.size();
        int maxi=1;
        string ans="";
        ans+=s[0];

        for(int i=0;i<n;i++){
            string odd=expand(s,i,i);
            string even=expand(s,i,i+1);

            if(odd.size()>maxi){
                maxi=odd.size();
                ans=odd;
            }
            if(even.size()>maxi){
                maxi=even.size();
                ans=even;
            }
            

        }
        return ans;
    }
};
```

## Complexity Analysis

### Approach 1: Dynamic Programming
- **Time Complexity**: $O(N^2)$ as we compute DP transitions for all possible substrings.
- **Space Complexity**: $O(N^2)$ to store the 2D DP grid.

### Approach 2: Expand Around Center
- **Time Complexity**: $O(N^2)$ in the worst case (e.g., all same characters).
- **Space Complexity**: $O(1)$ auxiliary space, as no extra arrays or tables are allocated.

---
**Key Takeaways**:
- **Substring Capture**: Finding the longest palindromic substring requires tracking indices (`start` and `length`) during state verification to construct the final substring.
- **Space-Efficient Expansion**: Center expansion runs with an identical time complexity of $O(N^2)$ but drops the space complexity to $O(1)$, which is highly preferred for memory efficiency.
