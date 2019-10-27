---
layout     : post
title      : "[LeetCode]Oct 2019, week 4"
date       : 2019-10-27 14:00:00
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

## Two Sum -- easy
#### Description :  
>Given an array of integers, return indices of the two numbers such that they add up to a specific target.You may assume that each input would have exactly one solution, and you may not use the same element twice.  

#### Example :  

    Given nums = [2, 7, 11, 15], target = 9,
    Because nums[0] + nums[1] = 2 + 7 = 9,
    return [0, 1].

#### Submission

    class Solution {
        fun twoSum(nums: IntArray, target: Int): IntArray {
            val map = HashMap<Int,Int>()
            for(i in nums.indices){
                var left = target - nums[i]
                if(map.containsKey(left)){
                   return intArrayOf(map[left]!!,i)
                }
                map[nums[i]]=i
            }
            return intArrayOf()
        }
    }

#### Logic
1. Create a map, which is to store iterated element.
2. Loop through all elements in given array and substrat target by current element, if remain already exist in map then return answer, else, put current element into map.

---
