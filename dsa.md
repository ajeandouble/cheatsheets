# DSA

## Resources

[How to self-study with Feynman Technique - youtube](https://www.youtube.com/watch?v=1O6qAssKqlU)
[Top 7 algorithms for coding interview - youtube](https://www.youtube.com/watch?v=guKRryH1yho)

## Greedy

At each step, the **locally optimal choice** is made without considering the overall consequences. The algorithm makes the choice that appears to be the best in the ***current situation***, hoping that it will lead to a globally optimal solution. Greedy algorithms solution **can be suboptimal**.

### Resources


## Dynamic Programming


### Resources

[DP (Max - Min) problems - leetcode](https://leetcode.com/list/55ac4kuc/)
[DP problems list - leetcode](https://leetcode.com/list/55ac4kuc/)
[DP Patterns - leetcode](https://leetcode.com/discuss/study-guide/458695/Dynamic-Programming-Patterns)


### Knapsack problem

### Coin change problem

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


## Strings

### Hashing

#### Polynomial Hashing


## Two Pointers


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


