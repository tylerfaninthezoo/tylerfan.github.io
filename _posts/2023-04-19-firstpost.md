---
layout: post
title: leetcode 1947
date: 2023-04-19 22:20:00
category: dp with bitmask
---

# Question

<p>
There is a survey that consists of n questions where each question's answer is either 0 (no) or 1 (yes).

The survey was given to m students numbered from 0 to m - 1 and m mentors numbered from 0 to m - 1. The answers of the students are represented by a 2D integer array students where students[i] is an integer array that contains the answers of the ith student (0-indexed). The answers of the mentors are represented by a 2D integer array mentors where mentors[j] is an integer array that contains the answers of the jth mentor (0-indexed).

Each student will be assigned to one mentor, and each mentor will have one student assigned to them. The compatibility score of a student-mentor pair is the number of answers that are the same for both the student and the mentor.

For example, if the student's answers were [1, 0, 1] and the mentor's answers were [0, 0, 1], then their compatibility score is 2 because only the second and the third answers are the same.
You are tasked with finding the optimal student-mentor pairings to maximize the sum of the compatibility scores.

Given students and mentors, return the maximum compatibility score sum that can be achieved.
</p>

```

    class Solution {
public:
    int maxCompatibilitySum(vector<vector<int>>& students, vector<vector<int>>& mentors) {

        int sz = students.size();
        int sz2 = students[0].size();
        <font color="green">// dp represents the taken mentors, for example, 00001111 means the last 4 mentors are already used. </font>
        vector<int> dp(1 << sz, -1);

        return dfs(0, 0, dp, students, mentors, sz);
        
    }

    int score(vector<int>& s, vector<int>& m) {
        int cnt = 0;
        for(int i =0; i< s.size(); i++) {
            if(s[i] == m[i]) cnt++;
        }
        return cnt;

    }

    int dfs(int indexi, int mask, vector<int>& dp, vector<vector<int>>& students, vector<vector<int>>& mentors, int sz) {
        if(indexi >= sz) return 0;
        if(dp[mask] != -1) return dp[mask];
        
        
        int bit =1;
        for(int i=0; i<sz; i++) {
            
            if((mask & bit) == 0)
            dp[mask] = max(dp[mask], score(students[indexi], mentors[i]) + dfs(indexi+1, mask| bit,dp,students,mentors,sz));

            bit = bit << 1;
        }
        

        return dp[mask];
    }
    
};
 
```

since we have to pick the same number for student and mentor at any stage, and we are iterating student in order,  we only need one dimension dp to keep track of the taken mentor. 