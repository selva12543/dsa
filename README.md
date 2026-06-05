# Two Pointers & Contains Duplicate – Interview Pattern Guide

## 1. Two Pointers Pattern

The Two Pointers technique is commonly used when working with **sorted arrays**, pairs of values, or problems that require finding a relationship between two elements.

### Common Interview Clues

#### Case 1: Sorted Array + Target Sum

**How they word it:**

> "Given an array of integers that is already sorted in ascending order, find two numbers..."

**Recommended Approach:** Two Pointers

```text
left = 0
right = n - 1

while left < right:
    sum = nums[left] + nums[right]

    if sum == target:
        return answer
    elif sum < target:
        left += 1
    else:
        right -= 1
```

**Time Complexity:** O(n)
**Space Complexity:** O(1)

---

#### Case 2: Find Two Numbers That Add Up to Target Using O(1) Extra Space

**How they word it:**

> "Find the two numbers that add up to the target, but you must do it in O(1) auxiliary space."

**Recommended Approach:**

1. Sort the array.
2. Apply Two Pointers.

**Time Complexity:** O(n log n) (sorting)
**Space Complexity:** O(1)

---

#### Case 3: Return 1-Indexed Positions

**How they word it:**

> "Return the indices of the two numbers added by one. Your solution must be 1-indexed."

**Recommended Approach:** Two Pointers

The logic remains the same; simply return:

```text
[left + 1, right + 1]
```

instead of:

```text
[left, right]
```

---

#### Case 4: Sum Closest to Target

**How they word it:**

> "Find two numbers such that the sum is closest to the target."

**Recommended Approach:**

1. Sort the array.
2. Use Two Pointers.
3. Track the minimum difference encountered.

**Time Complexity:** O(n log n)
**Space Complexity:** O(1)

---

## 2. Contains Duplicate Pattern

The goal is to determine whether an array contains any duplicate values.

---

### Approach 1: HashSet (Recommended)

**Use this 95% of the time.**

This is the industry-standard solution because it runs in linear time.

```text
Create a HashSet

For each number:
    If already in set:
        return true
    Add to set

return false
```

**Time Complexity:** O(n)
**Space Complexity:** O(n)

#### When to Use

* Large datasets
* Production systems
* General interview situations

#### Why?

If you have millions of items, this approach completes quickly, while brute force may become extremely slow.

---

### Approach 2: Sorting

Use when memory is restricted.

```text
Sort array

For i from 1 to n-1:
    If nums[i] == nums[i-1]:
        return true

return false
```

**Time Complexity:** O(n log n)
**Space Complexity:** O(1)

#### When to Use

* Embedded systems
* Memory-constrained environments
* Situations where extra memory allocation is undesirable

#### Important Note

Sorting modifies the original array.

---

### Approach 3: Brute Force

Mainly useful for learning purposes.

```text
For every element:
    Compare with every other element

If match found:
    return true

return false
```

**Time Complexity:** O(n²)
**Space Complexity:** O(1)

#### When to Use

* Academic understanding
* Small datasets

#### Why Avoid It?

Quadratic growth becomes impractical as input size increases.

---

### Approach 4: In-Place Hashing (Index as Key)

A less commonly discussed but powerful technique.

#### Idea

Use the array indices themselves as a hash table.

This works when:

* Values fall within a known range.
* You are allowed to modify the array.

Example techniques include:

* Cyclic Sort
* Index Mapping
* Sign Marking

**Time Complexity:** O(n)
**Space Complexity:** O(1)

#### When to Use

* Numbers are constrained to a specific range.
* Extra memory is forbidden.
* The array can be modified.

#### Why It's Interesting

It achieves the best of both worlds:

* Linear Time: O(n)
* Constant Space: O(1)

However, it only works under specific constraints and is therefore less universally applicable than the HashSet solution.

---

# Quick Interview Cheat Sheet

| Problem Clue                               | Best Approach       |
| ------------------------------------------ | ------------------- |
| Sorted array + pair search                 | Two Pointers        |
| Pair sum with O(1) space                   | Sort + Two Pointers |
| Return 1-indexed answer                    | Two Pointers        |
| Closest pair sum                           | Sort + Two Pointers |
| Contains duplicate (general case)          | HashSet             |
| Contains duplicate (low memory)            | Sorting             |
| Contains duplicate (learning only)         | Brute Force         |
| Contains duplicate with constrained values | In-Place Hashing    |

---

## Rule of Thumb

### Two Sum Family

* Sorted array → Two Pointers
* Unsorted array → HashMap
* O(1) space requirement → Sort + Two Pointers

### Contains Duplicate Family

* Default choice → HashSet
* Memory constrained → Sorting
* Learning only → Brute Force
* Special constrained-value problems → In-Place Hashing
