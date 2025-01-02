# DSA

## Resources

[How to self-study with Feynman Technique - youtube](https://www.youtube.com/watch?v=1O6qAssKqlU)
[Top 7 algorithms for coding interview - youtube](https://www.youtube.com/watch?v=guKRryH1yho)

## Greedy

At each step, the **locally optimal choice** is made without considering the overall consequences. The algorithm makes the choice that appears to be the best in the ***current situation***, hoping that it will lead to a globally optimal solution. Greedy algorithms solution **can be suboptimal**.

### Resources


## Arrays and Hashing

### Polynomial hashing

[Polynomial Rolling Hash](https://byby.dev/polynomial-rolling-hash)


## Two Pointers

### Two Sums 2 - Array is Sorted

```python3
def twoSum(self, nums: List[int], target: int) -> List[int]:
    l, r = 0, len(nums) -1
    while r > 0 and  nums[0] + nums[r] > target:
        r -= 1
    while l < r:
        if nums[l] + nums[r] == target: return(l+1, r+1)
        elif nums[l] + nums[r] > target: r-= 1
        else: l += 1
```

## Dynamic Programming


### Resources and notes

[How do you guys get good at DP? - reddit](https://www.reddit.com/r/leetcode/comments/sv82tg/how_do_you_guys_get_good_at_dp/)
[DP for beginners - leetcode](https://leetcode.com/discuss/study-guide/662866/DP-for-Beginners-Problems-or-Patterns-or-Sample-Solutions)
[DP (Max - Min) problems - leetcode](https://leetcode.com/list/55ac4kuc/)
[DP problems list - leetcode](https://leetcode.com/list/55ac4kuc/)
[DP Patterns - leetcode](https://leetcode.com/discuss/study-guide/458695/Dynamic-Programming-Patterns)
[neetcode.io - roadmap](https://neetcode.io/roadmap])
[Dynamic Programming - Jeff Erickson - Algorithms](http://jeffe.cs.illinois.edu/teaching/algorithms/book/03-dynprog.pdf)

#### Mental model

>One thing that helped me was coming up with a recursive solution to the problem, then take a look at the parameters you are passing to the recursive function. Then check which parameters change between calls, those are likely the coordinate in your dp array/matrix.
>Understand how the recursive call generates its answer from the sub recursive calls, try to put that into an equation, like currentRes = f(subRes). That would be your DP build up equation.

[How do you guys get good at DP? - reddit](https://www.reddit.com/r/leetcode/comments/sv82tg/how_do_you_guys_get_good_at_dp/)

### Knapsack problem

### Coin change problem

### Longest increasing subsequence

```python
def lengthOfLIS(self, nums: List[int]) -> int:
    N = len(nums)
    length = [1] * N
    for k in range (0, N):
        for i in range(0, k):
            if (nums[i] < nums[k]):
                length[k] = max(length[k], length[i]+1)
    return length[-1]
```

[Longest Increasing Subsequence - leetcode 300](https://leetcode.com/problems/longest-increasing-subsequence/)

### Shortest common subsequence

### Longest common subsequence

### Longest increasing subsequence

### Matrix chain manipulation

### Partition problem

### Rod cutting

### Edit distance problem (Levenshtein)

```python
def minDistance(self, word1: str, word2: str) -> int:
    dp = [[j if i == 0 else 0 for j in range(0, len(word2)+1)] for i in range(0, len(word1)+1)]
    for i, r in enumerate(dp):
        r[0] = i

    for i in range(1, len(word1)+1):
        for j in range(1, len(word2)+1):
            if word1[i-1] == word2[j-1]:
                dp[i][j] = dp[i-1][j-1]
            else:
                replace = dp[i-1][j-1]
                delete = dp[i][j-1]
                insert = dp[i-1][j]
                dp[i][j] = 1 + min(replace, delete, insert)

    return(dp[len(word1)][len(word2)])
```

[Edit Distance - leetcode 72](https://leetcode.com/problems/edit-distance/)

### Word break problem

### Kadane's Algorithm

[Maximum Subarray - leetcode #53](https://leetcode.com/problems/maximum-subarray/)


## Greedy


## Graphs
	
### Dijkstra


## Heap

### Priority Queue


## Sorting

### Topological sort

[Topological sort - youtube](https://www.youtube.com/watch?v=i9Uo7B1WiEE)

## Topics to sort

The Activity Selection Problem


