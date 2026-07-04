# Longest Common Subsequence

## Recursion + Memoization

```cpp
class Solution {
public:
    int f(int ind1,int ind2,string &text1 ,string &text2,vector<vector<int>>& dp){
        if(ind1==text1.size() || ind2==text2.size()) return 0;
        if(dp[ind1][ind2]!=-1) return dp[ind1][ind2];

        if(text1[ind1] == text2[ind2]) return dp[ind1][ind2]=1+f(ind1+1,ind2+1,text1,text2,dp);
        return dp[ind1][ind2]=max(f(ind1+1,ind2,text1,text2,dp),f(ind1,ind2+1,text1,text2,dp));
    }
    int longestCommonSubsequence(string text1, string text2) {
        int n=text1.size();
        int m=text2.size();
        vector<vector<int>> dp(n,vector<int>(m,-1));
        return f(0,0,text1,text2,dp);
    }
};
```
- Time complexity: $O(n*m)$
- Space complexity: $O(n*m)$

## Tabulation


```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int n=text1.size();
        int m=text2.size();
        vector<vector<int>> dp(n+1,vector<int>(m+1,0)); // LCS between Text1 of length i & Text2  of length 
        
        // Base case: LCS of any string with an empty string is 0. 
        // The first row and first column of dp table represents this base case, 
        // which are already initialized to 0.

        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                if(text1[i-1] == text2[j-1]) dp[i][j]=1+dp[i-1][j-1];
                else dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
            }
        }

        return dp[n][m];
    }
};
```
- Time complexity: $O(n*m)$
- Space complexity: $O(n*m)$


## Printing the LCS

```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int n=text1.size();
        int m=text2.size();
        vector<vector<int>> dp(n+1,vector<int>(m+1,0)); // LCS between Text1 of length i & Text2  of length 
        
        // Base case: LCS of any string with an empty string is 0. 
        // The first row and first column of dp table represents this base case, 
        // which are already initialized to 0.

        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                if(text1[i-1] == text2[j-1]) dp[i][j]=1+dp[i-1][j-1];
                else dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
            }
        }

        string lcs = "";
        int i=n,j=m;
        while(i>0 && j>0){
            if(text1[i-1] == text2[j-1]){
                lcs.push_back(text1[i-1]);
                i--;
                j--;
            }
            else if(dp[i-1][j] > dp[i][j-1]){
                i--;
            }
            else{
                j--;
            }
        }
        reverse(lcs.begin(),lcs.end());
        cout<<"LCS is: "<<lcs<<endl;

        return dp[n][m];
    }
};
```


