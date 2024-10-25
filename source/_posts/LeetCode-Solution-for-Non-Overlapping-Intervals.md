---
title: LeetCode Solution for Non Overlapping Intervals
date: 2024-10-24 23:28:55
categories: [LeetCode, Algorithm]
tags: [Insert Interval]
---

# Question:

Given an array of intervals intervals where intervals[i] = [starti, endi], return the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping.

Note that intervals which only touch at a point are non-overlapping. For example, [1, 2] and [2, 3] are non-overlapping.

## Explanation

移除数组中可能会导致重合的区间，找出最少的移除数量，注意如果只是区间的开头或者末尾与另一个数组开头或者结尾相同时不属于重合情况。

# Ideas:

1. 排序，以每个区间的结尾为排序标准进行升序排序
2. 比较: 如果下一个区间的开头 >= 前一个区间的结尾，说明此时不会重合 (初始化第一个区间的结尾作为衡量基准)，更新衡量基准为这个区间的结尾。如果大小关系不符，说明重合，此时移除区间的计数+1

# Code:

```python

def eraseOverlapIntervals(self, intervals: List[List[int]]) -> int:

    # sorted_intervals = intervals.sort(key = lambda x: x[1]): \ 这行代码错误原因是使用sort方法后，对原列表直接排序并返回None，所有此时sorted_intervals是None,无法进行后续的操作

    # Sort intervals in-place by their end
    intervals.sort(key=lambda x: x[1])

    count = 0

    # Initialize the end to the end value of the first interval
    end = intervals[0][1]

    # Start checking from the second interval
    for i in range(1, len(intervals)):
        # If the start time of the current interval is greater than or equal to the end of the previous one, they do not overlap
        if intervals[i][0] >= end:
            end = intervals[i][1]
        else:
            count += 1

    return count

```
