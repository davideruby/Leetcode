## [763. Partition Labels](https://leetcode.com/problems/partition-labels/)

<h2 style="color:#fac31d">Medium</h2>

You are given a string s. We want to partition the string into as many parts as possible so that each letter appears in at most one part.

Note that the partition is done so that after concatenating all the parts in order, the resultant string should be s.

Return a list of integers representing the size of these parts.

## Solution
```python
class Solution:
    def partitionLabels(self, s: str) -> List[int]:
        last_idx = {}
        for idx, char in enumerate(s):
            last_idx[char] = idx

        end = 0
        size = 0
        partition = []
        for idx, char in enumerate(s):
            size += 1
            end = max(end, last_idx[char])
            
            if idx == end:
                partition.append(size)
                size = 0
            
        return partition
```

## Notes
This is kinda a unique problem. 

First, we use a hashmap to store for each character the index where it occurs last.
Then, we loop over the string and use two pointers to keep track of each set of the partition: `size` and `end`. 
At each iteration, we increment `size` and we check the index where the current character appears last: that value should be the `end` of the current set of the partition. Then, if the index is equal to `end`, it means we got to the end of the set and we can add its size to the `partition` array.
