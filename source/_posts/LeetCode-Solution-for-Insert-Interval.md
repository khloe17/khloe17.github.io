---
title: LeetCode Solution for Insert Interval
date: 2024-10-24 23:28:55
categories: [LeetCode, Algorithm]
tags: [Insert Interval]
---

# Question:

You are given an array of non-overlapping intervals intervals where intervals[i] = [starti, endi] represent the start and the end of the ith interval and intervals is sorted in ascending order by starti. You are also given an interval newInterval = [start, end] that represents the start and end of another interval.

Insert newInterval into intervals such that intervals is still sorted in ascending order by starti and intervals still does not have any overlapping intervals (merge overlapping intervals if necessary).

Return intervals after the insertion.

## Explanation

给定一个已排序的、无重叠的区间列表 intervals，和一个新的区间 newInterval。目标是将 newInterval 插入到 intervals 中，并合并所有可能重叠的区间，最终返回一个没有重叠的、排序好的区间列表。

# Ideas:

1. 遍历 intervals：我们要找到 newInterval 可能会插入的位置。
2. 处理与新插入区间不重叠的区间：
   对于在 newInterval 左侧且没有重叠的区间，可以直接加入结果。
   对于在 newInterval 右侧且没有重叠的区间，同样可以直接加入结果。
3. 特殊情况：如果 intervals 为空，或者 newInterval 不与任何现有区间重叠，直接将其插入适当位置即可。

# Code:

```python

def insert(intervals, newInterval):
    result = []
    i = 0
    n = len(intervals)

    # Step1: Add all intervals that come before the newInterval
    while i < n and intervals[i][1] < newInterval[0]: \尚未遍历完所有区间, 并且当前区间的结束位置在新插入区间的开始位置之前, 即当前区间和新的区间完全没有重叠
        result.append(intervals[i])
        i += 1

    # Step2: Merge all overlapping intervals with newInterval
    while i < n and intervals[i][0] <= newInterval[1]:
        newInterval[0] = min(newInterval[0], intervals[i][0])
        newInterval[1] = max(newInterval[1], intervals[i][1])
        i += 1

    # Add the merged Interval
    result.append(newInterval)

    # Step3: Add all intervals that come after the newInterval
    while i < n: \ 此前，已经处理了在新插入区间之前的区间以及与新插入区间有重叠的区间，此时剩下的后面区间可以直接加入到结果中
        result.append(intervals[i])
        i += 1

    return result



```
