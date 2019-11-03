---
layout     : post
title      : "[LeetCode]Oct 2019, week 4 (Part 2)"
date       : 2019-11-03 13:00:00+08:00
author     : "Jimmy"
tags       : leetcode kotlin
comments   : true
signature  : true
---
# Summary of this week :
<span style="color:teal">easy</span> : 7  
<span style="color:orange">medium</span> : 0
<span style="color:red">hard</span> : 0
<!-- more -->

---

## Find All Numbers Disappeared in an Array -- easy
#### Description :
>Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.
>Find all the elements of [1, n] inclusive that do not appear in this array.
>Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

#### Example :

    Input:
    [4,3,2,7,8,2,3,1]

    Output:
    [5,6]

#### Submission

    class Solution {
      fun findDisappearedNumbers(nums: IntArray): List<Int> {
        val result = mutableListOf<Int>()
        val n = nums.size
        for(i in 0 until n) {nums[(nums[i]-1)%n]+=n}
        for(i in 0 until n) {if(nums[i]<=n) result.add(i+1)}
        return result
      }
    }

#### Logic
1. Loop through all elements in given array, for each element, add array size at index (element/array size).
2. After that, all elements in this array should have a new value which is greater than array length, if any of them is less than array size, which means the indices are disappeared in array.

---

## Jewels and Stones -- easy
#### Description :
>You're given strings J representing the types of stones that are jewels, and S representing the stones you have.  Each character in S is a type of stone you have.  You want to know how many of the stones you have are also jewels.
>The letters in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive, so "a" is considered a different type of stone from "A".

#### Example :

    #Example 1
    Input: J = "aA", S = "aAAbbbb"
    Output: 3

    #Example 2
    Input: J = "z", S = "ZZ"
    Output: 0

#### Submission

    class Solution {
      fun numJewelsInStones(J: String, S: String): Int =
        S.filter{it in J}.length
    }

#### Logic
1. For each character in S, if it exist in J, put it into a new array.
2. Return length of the new array

---

## Longest Common Prefix -- easy
#### Description :
>Write a function to find the longest common prefix string amongst an array of strings.
>If there is no common prefix, return an empty string "".

#### Example :

    #Example 1
    Input: ["flower","flow","flight"]
    Output: "fl"

    #Example 2
    Input: ["dog","racecar","car"]
    Output: ""
    Explanation: There is no common prefix among the input strings.

#### Submission

    class Solution {
      fun longestCommonPrefix(strs: Array<String>): String {
        var result = ""
        if(strs.isEmpty()) return result

        var minLength = Int.MAX_VALUE
        for(str in strs){
            minLength = Math.min(str.length,minLength)
        }

        for(i in 0 until minLength){
            var c = strs[0][i]
            for(j in 0 until strs.size){
                if(strs[j][i]!=c) return result
            }
            result += c
        }
        return result
      }
    }

#### Logic
1. Figure out the shortest string in given array, and set its length as minLength.
2. Take the first string as default in given array, then in each string loop through characters, if the character is same with default then add it to result

---

## Implement strStr() -- easy
#### Description :
>Implement strStr().
>Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

#### Example :

    #Example 1
    Input: haystack = "hello", needle = "ll"
    Output: 2

    #Example 2
    Input: haystack = "aaaaa", needle = "bba"
    Output: -1

#### Submission

    class Solution {
      fun strStr(haystack: String, needle: String): Int {
        if(needle.isNullOrEmpty()) return 0
        else if(!haystack.contains(needle)) return -1
        else return haystack.split(needle)[0].length
      }
    }

#### Logic
1. If needle is empty string, return 0.
2. If needle exist in haystack, split haystack with needle, then length of first string should be the index where first needle is, else return -1 means needle not exist in haystack.

---
