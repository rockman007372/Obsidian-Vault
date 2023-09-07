---
tags: counting 
aliases: 
date: 2022-07-24 Sunday
---

## Definition

>[!definition]
> A permutation represents the number of ways to arrange r objects out of n objects

Eg: Number of ways to rearrage 1, 2, 3 into distinct numbers = 3! = $3 * 2 * 1$ = 6

## Permutation formula

$${}^{n} P _{k} = \frac{n!}{(n-k)!} = n(n - 1)(n - 2)...(n - k + 1)$$

Special case: When k = n, ${}^{n} P _{k} = n!$ (number of ways to arrange n objects in order)

$${}^{n} P _{k} = {k! * {{n}\choose{k}}}$$

--- 
For LeetCode question: [[Permutation (Leet)]]
Tags: [[ST2334]] - [[Combination]]
