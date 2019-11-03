---
layout     : post
title      : "[LeetCode]Oct 2019, week 4 (Part 1)"
date       : 2019-10-27 14:00:00+08:00
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

## Two Sum II - Input array is sorted -- easy
#### Description :  
>Given an array of integers that is already sorted in ascending order, find two numbers such that they add up to a specific target number.
>The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2.  

#### Example :  

    Input: numbers = [2,7,11,15], target = 9
    Output: [1,2]
    Explanation: The sum of 2 and 7 is 9. Therefore index1 = 1, index2 = 2.

#### Submission

    class Solution {
      fun twoSum(numbers: IntArray, target: Int): IntArray {
        val map = HashMap<Int,Int>()
        for(i in numbers.indices){
          var left = target - numbers[i]

          if(map.containsKey(left)){
            return intArrayOf(map[left]!!+1,i+1)
          }
          map[numbers[i]]=i
        }
        return intArrayOf()
      }
    }

#### Logic
1. This problem is really familiar with "Two Sum", the only thing need to notice is the index1 of answer should be less than index2.
2. Since the logic I used in "Two Sum" and numbers sorted already, if var left exist in map, it must be equal or smaller than numbers[i], so the return value should be (index of left,index of numbers[i])

---

## Best Time to Buy and Sell Stock -- easy
#### Description :  
>Say you have an array for which the ith element is the price of a given stock on day i.
>If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.
>Note that you cannot sell a stock before you buy one.

#### Example :  

    Example 1
    Input: [7,1,5,3,6,4]
    Output: 5
    Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
                 Not 7-1 = 6, as selling price needs to be larger than buying price.

    Example 2
    Input: [7,6,4,3,1]
    Output: 0
    Explanation: In this case, no transaction is done, i.e. max profit = 0.

#### Submission

    class Solution {
      fun maxProfit(prices: IntArray): Int {
          var minprice = Int.MAX_VALUE
          var maxprofit = 0
          for(i in 0..(prices.size-1)){
              if(prices[i]<minprice){
                  minprice = prices[i]
              }else if (prices[i]-minprice>maxprofit){
                  maxprofit = prices[i]-minprice
              }
          }
          return maxprofit
      }
    }

#### Logic
1. Create 2 variants "minprice" & "maxprofit". As common, minprice is less the better and maxprofit is opposite.
2. So, iterated all prices, if the price is smaller then minprice, set minprice as current price.
3. Otherwise, if the price minus minprice is bigger than maxprofit, set maxprofit as the difference.
4. If the price doesn't match each of above conditions, just go to next one.
