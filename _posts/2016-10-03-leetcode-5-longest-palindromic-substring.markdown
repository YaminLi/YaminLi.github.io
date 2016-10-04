---
layout:     post
title:      "[Leetcode] 5. Longest Palindromic Substring"
subtitle:   "find the longest palindromic substring in S"
date:       2016-10-03 21:30:00
author:     "Michael"
header-img: "img/in-post/2016-10-03/bg1.jpg"
tags:
  - Leetcode
  - C++
---

## 1. Problem Definition

[Leetcode 5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)

> Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

Palindromic string means that it's the same as reversed one. For example, '12321', 'a', 'abba', and so on.

## 2. Solution  

<p></p>

#### 2.1 Brute-Force ####

For each substring of S, check whether it's a valid palindrome, and find the longest one. Assuming that there's n characters in S, so S has n^2 substrings totally and the average length of those substrings is n/2. So the whole runtime for brute-force algorithm is O(n^3).

````
class Solution{
public:
    string brute_force(string s){
        string res;
        int maxLen=0;
        for(int len = 1; len<=s.length(); len++){
            for(int i=0; i+len<=s.length(); i++){
                string subs = s.substr(i, len);
                if (isPalindromic(subs) && len>maxLen) {
                    maxLen = len;
                    res = subs;
                }
            }
        }
        return res;
    }

private:
    bool isPalindromic(string s){
        if (s.length() <= 1) {
            return true;
        }
        else{
            int i=0;
            int j=s.length()-1;
            while (j >= i ) {
                if (s[i] != s[j]) {
                    return false;
                }
                i++;
                j--;
            }
            return true;
        }
    }
};
````

#### 2.2 A little Better than Brute-Force ####

Because all the palindrome are symmetric, if the length of a palindrome one is even, then the symmetry axis locates between the middle two characters, otherwise it locates on the middle character. We can use the the symmetry axis to improve our algorithm's runtime. For each location of the symmetry axis, we look left and right at the same time till we meets the different left and right characters or reach the boundary. For a string with length n, there are n+n-1=2n-1 different locations of symmetry axis, and for each location, there are n/4 comparisons averagely. So the runtime is O(n^2).

````
class Solution{
public:
  string longestPalindrome(string s){
      string res;
      int maxLen = 0;
      for(int i=0; i<s.size(); i++){
          // palindrome's length is even
          for (int len=1; i-len>=0 && i+len-1<s.size(); len++) {
              string subs = s.substr(i-len, 2*len);
              if(isPalindromic(subs) && 2*len>maxLen){
                  maxLen = 2*len;
                  res = subs;
              }
          }
          // palindrome's length is odd
          for (int len=0; i-len>=0 && i+len<s.size(); len++) {
              string subs = s.substr(i-len, 2*len+1);
              if (isPalindromic(subs) && (2*len+1)>maxLen) {
                  maxLen = 2*len+1;
                  res = subs;
              }
          }
      }
      return res;
  }

private:
    bool isPalindromic(string s){
        if (s.length() <= 1) {
            return true;
        }
        else{
            int i=0;
            int j=s.length()-1;
            while (j >= i ) {
                if (s[i] != s[j]) {
                    return false;
                }
                i++;
                j--;
            }
            return true;
        }
    }
};
````

#### 2.3 Manacher ####

To be Continued

#### 2.4 Dynamic Programming ####

For each start point of the Palindromic substring, to check whether it's valid. And use a n*n array to memorize the palindromic status of the substring we have checked.

![img](/img/in-post/2016-10-03/bg.gif)
<!--
<span class="caption text-muted">To go places and do things that have never been done before – that’s what living is all about.</span> -->


````
class Solution{
public:
  string longestPalindrome2(string s){
        int n=s.length();
        bool isPalindrome[1000][1000]={false};
        int start = 0;
        int maxLen = 1;
        for (int i=n-1; i>=0; i--) {
            for (int j=i; j<n; j++) {
                if (s[i]==s[j] && (i+1>j-1 || isPalindrome[i+1][j-1])) {
                    isPalindrome[i][j] = true;
                    if (j-i+1 > maxLen) {
                        maxLen = j-i+1;
                        start = i;
                    }
                }
            }
        }
        return s.substr(start, maxLen);
    }
};
````
