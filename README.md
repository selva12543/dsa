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


# =================================================================================================================================================================

# Group Anagrams (Java) - Complete Interview Guide

The **Group Anagrams** problem is an absolute classic in coding interviews. It is one of those foundational problems that bridges the gap between basic data structures and clever algorithmic thinking.

This guide will help you understand the problem, why interviewers ask it, and the key concepts needed to solve it efficiently in Java.

---

## 1. What is the Problem?

An **anagram** is a word formed by rearranging the letters of another word while using all original letters exactly once.

### Example

```text
"eat", "tea", and "ate"
```

All three words contain the same characters and are therefore anagrams of each other.

### Problem Statement

Given an array of strings, group all anagrams together.

### Input

```java
["eat", "tea", "tan", "ate", "nat", "bat"]
```

### Output

```java
[
    ["eat", "tea", "ate"],
    ["tan", "nat"],
    ["bat"]
]
```

---

## 2. Why is This Problem Important?

The Group Anagrams problem is frequently asked because it tests several fundamental programming concepts.

### What It Evaluates

#### 1. Data Structures

Interviewers assess your understanding of:

* HashMap
* Arrays
* Strings
* Lists

#### 2. Pattern Recognition

You must identify a way to create a **unique identifier (key)** for words that are anagrams of each other.

For example:

```text
eat → aet
tea → aet
ate → aet
```

Since all three produce the same sorted representation, they belong to the same group.

#### 3. Optimization Skills

There are multiple ways to solve this problem:

* Brute-force approach (very slow)
* Sorting-based approach (efficient)
* Character frequency approach (more optimized)

Interviewers want to see whether you can move from a naive solution to an efficient one.

---

## 3. Why Interviewers Love This Question

This problem is popular because it combines:

* Hashing
* String manipulation
* Array processing
* Time complexity analysis

It quickly reveals whether a candidate can:

* Choose the right data structure
* Design a smart key-generation strategy
* Write clean and efficient code

---

## 4. How Interviewers Might Frame the Question

Interviewers do not always directly ask:

> "Write a program to group anagrams."

Instead, they often disguise the problem in real-world scenarios.

### Example 1: Word Game

> You are building a feature for a word game where users get points for finding scrambled words. Group the user inputs by their base letters.

### Example 2: Username Analysis

> Given a list of usernames, group together users who used the exact same characters in their handles.

### Example 3: Dictionary Processing

> Organize words into clusters where each cluster contains words made from the same set of letters.

Even though the wording changes, the underlying concept remains the same:

**Group strings that contain identical characters.**

---

## Key Takeaway

The Group Anagrams problem teaches one of the most important interview patterns:

> Transform each item into a canonical form and use a HashMap to group similar items efficiently.

Mastering this pattern will help you solve many other interview problems involving:

* Hashing
* String manipulation
* Frequency counting
* Data grouping
* Pattern matching

It is a must-know problem for coding interviews at companies ranging from startups to FAANG-level organizations.


## 2. How to Spot the Pattern

Whenever you see a problem asking you to **group**, **categorize**, or **collect** items based on a shared characteristic, your brain should immediately think:

> **HashMap**

The key insight in the **Group Anagrams** problem is finding a **universal key**.

Even though words like `"eat"` and `"tea"` are spelled differently, they need to generate the **same key** so they can be placed into the same bucket in our HashMap.

There are multiple ways to generate this key, which leads us to different solution approaches.

---

## 3. Method 1: Categorize by Sorting (The Intuitive Way)

### Core Idea

If you sort the letters of an anagram alphabetically, all anagrams become the exact same string.

#### Example

```text
"eat" → "aet"
"tea" → "aet"
"ate" → "aet"
```

Since all anagrams produce the same sorted result, we can use the **sorted string as the HashMap key**.

### Algorithm

1. Create an empty HashMap.
2. For each word:

   * Sort its characters.
   * Use the sorted string as the key.
   * Add the original word to the list associated with that key.
3. Return all the values from the HashMap.

### Visualization

```text
Input:
["eat", "tea", "tan", "ate", "nat", "bat"]

HashMap:

"aet" → ["eat", "tea", "ate"]
"ant" → ["tan", "nat"]
"abt" → ["bat"]
```

### Why It Works

All anagrams contain the same characters with the same frequencies.

Sorting rearranges those characters into a consistent order, causing every anagram in the group to generate an identical key.

### Time Complexity

* Sorting each word: O(k log k)
* For n words: O(n × k log k)

Where:

* n = number of words
* k = average length of each word

### Space Complexity

```text
O(n × k)
```

For storing the HashMap and grouped anagrams.

## Method 1: Categorize by Sorting

### Idea

Two strings are anagrams if their sorted forms are identical.

For example:

* `"eat"` → `"aet"`
* `"tea"` → `"aet"`

Since both produce the same sorted string, they belong to the same group.

### Java Code

```java
import java.util.*;

public class GroupAnagramsSorting {
    public List<List<String>> groupAnagrams(String[] strs) {
        // Map to store: SortedString -> List of Original Strings
        Map<String, List<String>> map = new HashMap<>();

        for (String s : strs) {
            // 1. Convert string to character array and sort it
            char[] charArray = s.toCharArray();
            Arrays.sort(charArray);
            String sortedKey = new String(charArray);

            // 2. If the key doesn't exist, create a new list
            if (!map.containsKey(sortedKey)) {
                map.put(sortedKey, new ArrayList<>());
            }

            // 3. Add the original string to the corresponding list
            map.get(sortedKey).add(s);
        }

        // Return all the grouped lists
        return new ArrayList<>(map.values());
    }
}
```

### Complexity Analysis (Beginner Level)

Let:

* **N** = Total number of strings
* **K** = Maximum length of a string

#### Time Complexity: O(N × K log K)

We loop through all **N** words.

For each word, sorting its characters takes **O(K log K)** time.

Therefore:

```
O(N × K log K)
```

#### Space Complexity: O(N × K)

We store all words inside the HashMap and the resulting grouped lists.

---

# Method 2: Categorize by Frequency Count (Optimal Approach)

### Idea

Sorting takes **O(K log K)** time.

Since the strings contain only lowercase English letters (`a-z`), we can count the frequency of each character.

Two words are anagrams if and only if their character frequencies are identical.

Example:

```
eat → a=1, e=1, t=1
tea → a=1, e=1, t=1
```

Both have the same frequency distribution, so they belong to the same group.

Instead of sorting, we create a unique key from the frequency counts.

Example key:

```
#1#0#0#0#1#0...#1
```

### Java Code

```java
import java.util.*;

public class GroupAnagramsCount {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();

        for (String s : strs) {
            // Array to count frequency of each character (a-z)
            int[] count = new int[26];

            for (char c : s.toCharArray()) {
                count[c - 'a']++;
            }

            // Convert frequency array into a unique string key
            StringBuilder sb = new StringBuilder();

            for (int freq : count) {
                sb.append('#');
                sb.append(freq);
            }

            String key = sb.toString();

            // Group strings by key
            if (!map.containsKey(key)) {
                map.put(key, new ArrayList<>());
            }

            map.get(key).add(s);
        }

        return new ArrayList<>(map.values());
    }
}
```

### Complexity Analysis (Beginner Level)

#### Time Complexity: O(N × K)

We examine every character exactly once while counting frequencies.

For each string:

```
Counting characters = O(K)
```

For N strings:

```
O(N × K)
```

This is faster than sorting because:

```
O(K) < O(K log K)
```

#### Space Complexity: O(N × K)

The HashMap stores all strings grouped by their frequency keys.

---

# Comparison Summary

| Method          | Time Complexity | Space Complexity | Best Used When                                            |
| --------------- | --------------- | ---------------- | --------------------------------------------------------- |
| Sorting         | O(N × K log K)  | O(N × K)         | Easy to understand and implement quickly in interviews    |
| Frequency Count | O(N × K)        | O(N × K)         | Better for long strings and when optimization is required |

---

# Key Takeaways

### Sorting Approach

✅ Simple and intuitive

✅ Easy to explain in interviews

❌ Slower because sorting takes O(K log K)

### Frequency Count Approach

✅ Optimal solution

✅ Avoids sorting completely

✅ Runs in O(N × K)

✅ Preferred when the interviewer asks for further optimization

### Interview Strategy

1. Start with the sorting solution.
2. Explain its complexity: O(N × K log K).
3. Then optimize using frequency counting.
4. Mention that frequency counting reduces the complexity to O(N × K).

This demonstrates both problem-solving ability and optimization skills.

# =================================================================================================================================================================
# Top K Frequent Elements (LeetCode 347)

This problem asks you to find the **k most frequent elements** in an integer array.

It is a classic interview problem that tests your understanding of:
- Frequency counting using HashMap
- Heap (Priority Queue) usage
- Bucket sort optimization
- Time-space tradeoffs

---

## 📌 Problem Statement

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements.

You may return the answer in **any order**.

---

## 🧠 How to Identify This Problem

You are likely dealing with a **Top K Frequent Elements** problem if you see:

### Keywords / Patterns:
- "most frequent"
- "top k elements"
- "k largest by frequency"
- "sort by count"
- "frequency of elements"

### Hidden signals:
- You need **counts of elements first**
- Then you need **ranking by frequency**
- Full sorting is usually **not required or too slow**
- Input size is large → expect **O(N log k) or O(N)** solution

### Core idea:
> This is a **frequency + selection problem**, not a simple sorting problem.

---

## 🚀 Approach 1: Min Heap (Priority Queue)

### 💡 Idea
1. Count frequency using a `HashMap`
2. Maintain a **min-heap of size k**
3. Keep only the top k frequent elements
4. Extract results from heap

### ⏱ Complexity
- Time: **O(N log k)**
- Space: **O(N)**

### ✅ Java Code

```java
import java.util.*;

public class Solution {
    public int[] topKFrequent(int[] nums, int k) {

        Map<Integer, Integer> frequencyMap = new HashMap<>();
        for (int num : nums) {
            frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
        }

        PriorityQueue<Integer> minHeap = new PriorityQueue<>(
            (a, b) -> frequencyMap.get(a) - frequencyMap.get(b)
        );

        for (int key : frequencyMap.keySet()) {
            minHeap.add(key);
            if (minHeap.size() > k) {
                minHeap.poll();
            }
        }

        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = minHeap.poll();
        }

        return result;
    }
}

# Top K Frequent Elements — Bucket Sort Approach (Most Optimal)

If you need the absolute fastest time complexity, the Bucket Sort method avoids the overhead of traversing a tree structure entirely.

---

## 🚀 Strategy

1. **Count frequencies**
   - Use a `HashMap` to store the frequency of each number.

2. **Create buckets**
   - Create an array of `List<Integer>` where:
     - Index = frequency of elements
   - Since a number can appear at most `N` times (where `N` is the length of the array), the bucket size is `N + 1`.

3. **Fill buckets**
   - Place each number into the bucket corresponding to its frequency.

4. **Collect results**
   - Traverse the bucket array from right to left (highest frequency → lowest)
   - Collect elements until you have `k` results.

---

## 💻 Java Implementation

```java
import java.util.*;

public class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        // Step 1: Build frequency map
        Map<Integer, Integer> countMap = new HashMap<>();
        for (int num : nums) {
            countMap.put(num, countMap.getOrDefault(num, 0) + 1);
        }

        // Step 2: Create buckets (index = frequency)
        List<Integer>[] buckets = new List[nums.length + 1];

        for (int key : countMap.keySet()) {
            int frequency = countMap.get(key);

            if (buckets[frequency] == null) {
                buckets[frequency] = new ArrayList<>();
            }

            buckets[frequency].add(key);
        }

        // Step 3: Gather top k frequent elements
        int[] result = new int[k];
        int index = 0;

        for (int i = buckets.length - 1; i >= 0 && index < k; i--) {
            if (buckets[i] != null) {
                for (int num : buckets[i]) {
                    result[index++] = num;
                    if (index == k) {
                        return result;
                    }
                }
            }
        }

        return result;
    }
}

# ⏱️ Complexity Analysis

## Time Complexity

**O(N)**

- Building frequency map → O(N)  
- Filling buckets → O(N)  
- Traversing buckets → O(N)  

## Space Complexity

**O(N)**

- Frequency map + bucket array  

---

# 📌 Summary: Which One Should You Use?

## ✔️ Use Min-Heap when:
- Dataset is very large  
- k is small  
- You want a general-purpose, widely applicable solution  

**Complexity:** O(N log k)

---

## ✔️ Use Bucket Sort when:
- You need strict linear time performance  
- Data is bounded and frequency-based grouping is efficient  

**Complexity:** O(N) *(fastest possible in this case)*
