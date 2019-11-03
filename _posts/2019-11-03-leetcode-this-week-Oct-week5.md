---
layout     : post
title      : "[LeetCode]Oct 2019, week 5"
date       : 2019-11-03 16:00:00+08:00
author     : "Jimmy"
tags       : leetcode kotlin
comments   : true
signature  : true
---
# Summary of this week :
<span style="color:teal">easy</span> : 4  
<span style="color:orange">medium</span> : 1
<span style="color:red">hard</span> : 0
<!-- more -->

---

## Maximize Sum Of Array After K Negations -- easy
#### Description :
>Given an array A of integers, we must modify the array in the following way: we choose an i and replace A[i] with -A[i], and we repeat this process K times in total.  (We may choose the same index i multiple times.)
>Return the largest possible sum of the array after modifying it in this way.

#### Example :

    #Example 1
    Input: A = [4,2,3], K = 1
    Output: 5
    Explanation: Choose indices (1,) and A becomes [4,-2,3].

    #Example 2
    Input: A = [3,-1,0,2], K = 3
    Output: 6
    Explanation: Choose indices (1, 2, 2) and A becomes [3,1,0,2].

    #Example 3
    Input: A = [2,-3,-1,5,-4], K = 2
    Output: 13
    Explanation: Choose indices (1, 4) and A becomes [2,3,-1,5,4].

#### Submission

    class Solution {
      fun largestSumAfterKNegations(A: IntArray, K: Int): Int {
        A.sort()
        for(i in K downTo 1){
            if(A[K-i]<0){
                A[K-i] = -A[K-i]
            }else if(i%2==1){
                A.sort()
                A[0] = -A[0]
                break
            }else break
        }
        return A.sum()
      }
    }

#### Logic
1. Sorting given array, so the negative ones (if exist) will in the front of array.
2. Loop through sorted array with K times, in each k time, check if the element at index k is negative, if it is then switch it to positive.
3. If current element is not negative, which mean all elements are positive now, so if left times j is odd, change the smallest one, otherwise break the looping.
4. Return summary of this array.

---

## First Unique Character in a String -- easy
#### Description :
>Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

#### Example :

    #Example 1
    s = "leetcode"
    return 0.

    #Example 2
    s = "loveleetcode",
    return 2.

#### Submission

    class Solution {
      fun firstUniqChar(s: String): Int {
        val pairs = hashMapOf<Char,Int>()
        s.forEach{c->
            pairs[c] = pairs.getOrDefault(c,0) + 1
        }
        for(c in s){
            if(pairs[c]==1)return s.indexOf(c)
        }
        return -1
      }
    }

#### Logic
1. Split given string to individual characters and counts appeared times for each characters.
2. Loop through each character in string, if the appeared time is 1 then return index of this character, if all characters appeared more than 1 time, return -1.

---

## Valid Anagram -- easy
#### Description :
>Given two strings s and t , write a function to determine if t is an anagram of s.

#### Example :

    #Example 1
    Input: s = "anagram", t = "nagaram"
    Output: true

    #Example 2
    Input: s = "rat", t = "car"
    Output: false

#### Submission

    class Solution {
      fun isAnagram(s: String, t: String): Boolean {
        if(s.length != t.length) return false

        val sArray = IntArray(26){i->0}
        val tArray = IntArray(26){i->0}
        for(i in 0 until s.length){
            sArray[s[i].toInt()-97]++
            tArray[t[i].toInt()-97]++
        }
        for(i in 0..25){
            if(sArray[i]!=tArray[i])return false
        }
        return true
      }
    }

#### Logic
1. Check length of two strings, if them are with different length then of course t is not an anagram of s.
2. Create two arrays with 26 '0' to counts which character appeared times.
3. Compare these two arrays step by step, if any elements of them are different, then t is not an anagram of s.

---

## Majority Element -- easy
#### Description :
>Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.
>You may assume that the array is non-empty and the majority element always exist in the array.

#### Example :

    #Example 1
    Input: [3,2,3]
    Output: 3

    #Example 2
    Input: [2,2,1,1,1,2,2]
    Output: 2

#### Submission
After submissed, the runtime is really bad for my answer, so I take a look with the fastest one, and the answer is really brilliant so I want to share it as well and explain the logic.

###### My Answer :  

    class Solution {
      fun majorityElement(nums: IntArray): Int {
        val major = nums.size/2
        val pairs = hashMapOf<Int,Int>()
        nums.forEach{e->
            pairs[e] = pairs.getOrDefault(e,0)+1
        }
        pairs.forEach{(k,v)->
            if(v > major) return k
        }
        return -1
      }
    }

###### Awesome Answer :  

    class Solution {
      fun majorityElement(nums: IntArray): Int {
        nums.sort()
        return nums[nums.size/2]
      }
    }

#### Logic
1. Sorting the array, as the description said the majority element always exist, so the element exist in the middle must be the majority one.

---

## Grumpy Bookstore Owner -- medium
#### Description :
>Today, the bookstore owner has a store open for customers.length minutes.  Every minute, some number of customers (customers[i]) enter the store, and all those customers leave after the end of that minute.
>On some minutes, the bookstore owner is grumpy.  If the bookstore owner is grumpy on the i-th minute, grumpy[i] = 1, otherwise grumpy[i] = 0.  When the bookstore owner is grumpy, the customers of that minute are not satisfied, otherwise they are satisfied.
>The bookstore owner knows a secret technique to keep themselves not grumpy for X minutes straight, but can only use it once.
>Return the maximum number of customers that can be satisfied throughout the day.

#### Example :

    Input: customers = [1,0,1,2,1,1,7,5], grumpy = [0,1,0,1,0,1,0,1], X = 3
    Output: 16
    Explanation: The bookstore owner keeps themselves not grumpy for the last 3 minutes.
    The maximum number of customers that can be satisfied = 1 + 1 + 1 + 1 + 7 + 5 = 16.

#### Submission

    class Solution {
      fun maxSatisfied(customers: IntArray, grumpy: IntArray, X: Int): Int {
        if(customers.size != grumpy.size || X > customers.size || X > grumpy.size)
            throw Exception()

        for(i in 0 until customers.size){
            if(grumpy[i]==1) customers[i] = -customers[i]
        }

        var index = 0
        var minScore = Int.MAX_VALUE
        for(i in 0 until customers.size-X+1){
            var score = 0
            for(j in 0 until X){
                if(customers[i+j] < 0) score += customers[i+j]
            }
            if(score < minScore){
                minScore = score
                index = i
            }
        }

        for(i in index until (index+X)){
            if(customers[i]<0) customers[i] = -customers[i]
        }

        return customers.filter{it>0}.sum()
      }
    }

#### Logic
Even though this is not a good practice (take too much runtime), but this is the first medium problem solved without looks discussion, so I'll keep it as a memory.
1. For customers of each minute, if owner was grumpy at that min, set customers value as negative one.
2. Use X as a window and iterate all changed customer values, counts the smallest negative values.
3. Set value in the window of smallest negative values as positive, then counts all positive values.
---
