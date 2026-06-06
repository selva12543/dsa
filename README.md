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

### Approach 4: In-Place Hashing (Index as Key) (can modify original array , but dont use extra memory) and (array not allowed to have 0)

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

  ```
  public static boolean anyDuplicateInPlace(int[] numbers) {
    boolean hasDuplicate = false;

    for (int i = 0; i < numbers.length; i++) {
        int index = Math.abs(numbers[i]) - 1;
        
        if (numbers[index] < 0) {
            hasDuplicate = true; 
            break; // Found it! Break early
        }
        numbers[index] = -numbers[index];
    }
    
    // CLEAN UP: Restore the original array by making everything positive again
    for (int i = 0; i < numbers.length; i++) {
        numbers[i] = Math.abs(numbers[i]);
    }
    
    return hasDuplicate;
}

  ```

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



# -----------------------------------------------------------------------------------------------------------------------------------------------------------------
# LeetCode 242: Valid Anagram (Java Guide)

An **anagram** is a word or phrase formed by rearranging the letters of another word or phrase using all original letters exactly once.

### Examples

* `"anagram"` → `"nagaram"` ✅
* `"rat"` → `"car"` ❌

---

## 🧠 Key Clue (How to Recognize the Problem)

If you notice:

* Order does **not** matter
* Only the **frequency of characters** matters
* You are comparing two strings or collections

👉 Think: **Frequency Counting Problem**

---

## 🚀 Best Approach (Recommended)

### 🥇 Fixed-Size Frequency Array (`int[26]`)

Use this approach when the input contains only lowercase English letters (`a-z`).

### Idea

1. Create an integer array of size 26.
2. Increment the count for each character in `s`.
3. Decrement the count for each character in `t`.
4. If all values are `0`, the strings are anagrams.

### Complexity Analysis

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(1)`

### Java Solution

```java
public class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        int[] count = new int[26];

        for (int i = 0; i < s.length(); i++) {
            count[s.charAt(i) - 'a']++;
            count[t.charAt(i) - 'a']--;
        }

        for (int num : count) {
            if (num != 0) {
                return false;
            }
        }

        return true;
    }
}
```

### Why This Is the Best Approach

* ⚡ Linear time complexity
* 🧠 Constant extra space
* 🔥 Fastest solution under standard LeetCode constraints

---

## ⚖️ Alternative Approaches

### 🥈 HashMap Method (Scalable for Unicode)

Use a dynamic map to track character frequencies.

This approach is useful when the input may contain:

* Uppercase letters
* Numbers
* Symbols
* Unicode characters (e.g., emojis)

### How It Works

1. Count frequencies of characters in `s`.
2. Subtract frequencies using `t`.
3. Verify all counts become `0`.

### Complexity Analysis

* **Time Complexity:** `O(n)`
* **Space Complexity:** `O(k)`

Where `k` is the number of unique characters.

### Java Solution

```java
import java.util.HashMap;

public class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        HashMap<Character, Integer> map = new HashMap<>();

        for (char c : s.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) + 1);
        }

        for (char c : t.toCharArray()) {
            map.put(c, map.getOrDefault(c, 0) - 1);
        }

        for (int value : map.values()) {
            if (value != 0) {
                return false;
            }
        }

        return true;
    }
}
```

---

### 🥉 Sorting Method (Simple & Intuitive)

Convert both strings into character arrays, sort them, and compare.

### How It Works

1. Convert strings into character arrays.
2. Sort both arrays.
3. Compare using `Arrays.equals()`.

### Complexity Analysis

* **Time Complexity:** `O(n log n)`
* **Space Complexity:** `O(n)`

### Java Solution

```java
import java.util.Arrays;

public class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) {
            return false;
        }

        char[] sChars = s.toCharArray();
        char[] tChars = t.toCharArray();

        Arrays.sort(sChars);
        Arrays.sort(tChars);

        return Arrays.equals(sChars, tChars);
    }
}
```

---

## 📌 Cheat Sheet

| Scenario                          | Recommended Approach        | Reason                            |
| --------------------------------- | --------------------------- | --------------------------------- |
| Lowercase English Letters (`a-z`) | Frequency Array (`int[26]`) | Fastest and most memory-efficient |
| Unicode / Emojis / Symbols        | HashMap                     | Supports dynamic character sets   |
| Quick Coding or Prototyping       | Sorting                     | Easiest to write and understand   |

---

## 🏁 Summary

| Approach        | Time         | Space  | Notes                          |
| --------------- | ------------ | ------ | ------------------------------ |
| Frequency Array | `O(n)`       | `O(1)` | Best for interview constraints |
| HashMap         | `O(n)`       | `O(k)` | Best for Unicode support       |
| Sorting         | `O(n log n)` | `O(n)` | Simplest implementation        |

### Recommendation

✅ Use **Frequency Array** for LeetCode interviews.

✅ Use **HashMap** when handling arbitrary character sets.

✅ Use **Sorting** when readability matters more than performance.
