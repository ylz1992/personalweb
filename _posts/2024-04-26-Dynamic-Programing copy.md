---
layout: post
title: Dynamic Programming
date: 2024-04-26
description: Coding
tags: Personal
categories: class
---
Base Model-Longest Common Subsequence: #1143, #712, #718，#583 
```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length();
        int n = text2.length();
        int[][] dp = new int[m+1][n+1];
        
        if (m == 0 || n==0){return 0;}
        for (int i=0;i<=m;i++){dp[i][0] = 0;};
        for (int i=0;i<=n;i++){dp[0][i] = 0;};
        for(int i=1;i<=m;i++){
            for(int j=1;j<=n;j++){
                if (text1.charAt(i-1)==text2.charAt(j-1)){
                    dp[i][j] = dp[i-1][j-1]+1;
                }
                else{
                    dp[i][j] = Math.max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }
    }
}
```
Base Model - Max Length: 
```java
//maxLength Problem, 
//Given an integer array nums, return the length of the longest strictly increasing
//subsequence
//Example 1:
//Input: nums = [10,9,2,5,3,7,101,18]
//Output: 4
//Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

class Solution {
    public int lengthOfLIS(int[] nums) {
        if(nums== null || nums.length ==0){return 0;}
        int n = nums.length;
        int[] dp = new int[n];
        int maxL = 0;
        for (int i =0;i<n;i++){
            dp[i] =1;
            for (int j =0;j<i;j++){
                if(nums[i]>nums[j]){
                    dp[i] = Math.max(dp[i],dp[j]+1);
                }
            }
            maxL = Math.max(maxL,dp[i]);
        }
        return maxL;
    }
}
```
Base Model- Unique Path: # 62, #63, #64
```java
//Unique Path
class Solution {
    private int m;
    private int n;
    private int[][] dp;
    public int uniquePaths(int m, int n) {
        this.m = m;
        this.n = n;
        this.dp = new int[m][n];
        return dfs(0,0);
    };
    private int dfs(int x,int y){
        if(x>m-1 || y>n-1){return 0;};
        if(x==m-1 && y==n-1){return 1;};
        if(dp[x][y]==0){return dp[x][y] =dfs(x+1,y) +dfs(x,y+1) ;};
        return dp[x][y];
    };
    
```
```java
//Min path sum
No.64 DP shortest path

class Solution {
    public int minPathSum(int[][] grid) {
        int row = grid.length;
        //if(row == 0){return 0;};
        int col = grid[0].length;
        
        for (int r = 0;r<row;r++){
            for(int c = 0;c<col;c++){
                if(r == 0 && c == 0){continue;}
                else if(r == 0){ grid[r][c] += grid[r][c-1];}
                else if(c == 0){grid[r][c] += grid[r-1][c];}
                else{grid[r][c] += Math.min(grid[r-1][c],grid[r][c-1]);}
            }

        }
        return grid[row-1][col-1];

    }
}
```
Base Model-Dp for Max square (filled with 1): #221, # 304, #85
```java
DP for max square.
  
class Solution {
    public int maximalSquare(char[][] matrix) {
        if(matrix == null || matrix.length ==0 || matrix[0].length == 0){return 0;}
        int m = matrix.length;
        int n = matrix[0].length;
        int[][]dp = new int[m+1][n+1];
        int maxS=0;
        for (int i=1;i<=m;i++){
            for (int j=1;j<=n;j++){
                if(matrix[i-1][j-1]=='1'){
                    dp[i][j] = Math.min(Math.min(dp[i-1][j],dp[i][j-1]),dp[i-1][j-1])+1;
                    maxS = Math.max(maxS, dp[i][j]);
                }

            }
        }
        return maxS * maxS;
    }
}
```
Base Model-House Robber: #198, #740, #213, #309,#790,#801
```java
//maximize the number of points nums[i], while delete nums[i-1]
class Solution {
    public int deleteAndEarn(int[] nums) {
        if (nums == null || nums.length == 0){return 0;}
        int max = 0;
        for (int num: nums){
            max = Math.max(max, num);
        }
        int[] points = new int[max+1];
        for (int num: nums){
            points[num] += num;
        }
        int[] dp = new int[max+1];
        dp[0] = points[0];
        dp[1] = Math.max(points[0],points[1]);
        for (int i=2;i<=max;i++){
            dp[i] = Math.max(dp[i-1],dp[i-2]+ points[i]);
        }
        return dp[max];

```
```java
DP, rob1, rob2 keep track of the maximum money robbed up to two steps back and one step back
class Solution {
    public int rob(int[] nums) {
        if(nums == null || nums.length ==0){return 0;}
        else if(nums.length ==1){return nums[0];}
        else if(nums.length ==2){return Math.max(nums[0],nums[1]);}
        return Math.max(robLinear(nums,0,nums.length -2), robLinear(nums,1,nums.length -1));

    }
    private int robLinear(int[] nums, int start, int end){
        int rob1 =0, rob2=0;
        for (int i = start; i<= end; i++){
            int newRob = Math.max(rob1 + nums[i], rob2);
            rob1  = rob2;
            rob2 = newRob;
        }
        return rob2;
    }
}
```

