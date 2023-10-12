# leet-day89

# Find in Mountain Array

## Description

You are given a mountain array and a target value. A mountain array is defined as an array that:
- Has at least three elements.
- There exists some `i` (0 < i < `length - 1`) such that `arr[0] < arr[1] < ... < arr[i - 1] < arr[i]` and `arr[i] > arr[i + 1] > ... > arr[length - 1]`.

You are asked to find the index of the target value in the mountain array. If the target value is not found, return -1.

You can only access the array using a provided MountainArray interface, which has two methods:
- `int get(int index)` to get the value at a specific index.
- `int length()` to get the length of the array.

## Approach

The approach to solve this problem involves binary searching for the peak of the mountain array and then performing binary searches on both sides of the peak.

1. **Finding the Peak**: Use binary search to find the index of the peak element. This is the highest point in the mountain.

2. **Searching on the Left Side**: Perform a binary search on the left side of the peak (from index 0 to the peak index) to find the target value.

3. **Searching on the Right Side**: Perform a binary search on the right side of the peak (from the peak index + 1 to the end) to find the target value.

4. **Result**: If the target value is found on either side, return the index; otherwise, return -1.

## Pseudocode

Here's a pseudocode for the above approach:

```
function findInMountainArray(target, mountainArray):
    n = mountainArray.length()

    # Binary search to find the peak
    left = 0
    right = n - 1
    while left < right:
        mid = left + (right - left) / 2
        if mountainArray.get(mid) < mountainArray.get(mid + 1):
            left = mid + 1
        else:
            right = mid

    peak = left

    # Binary search on the left side
    left = 0
    right = peak
    while left <= right:
        mid = left + (right - left) / 2
        val = mountainArray.get(mid)
        if val == target:
            return mid
        elif val < target:
            left = mid + 1
        else:
            right = mid - 1

    # Binary search on the right side
    left = peak + 1
    right = n - 1
    while left <= right:
        mid = left + (right - left) / 2
        val = mountainArray.get(mid)
        if val == target:
            return mid
        elif val > target:
            left = mid + 1
        else:
            right = mid - 1

    return -1  # If target is not found
```

## Complexity Analysis

- Time complexity: O(log n), where `n` is the length of the mountain array.
- Space complexity: O(1) - Constant space.
