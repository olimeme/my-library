# Chapter 1

## Algorithms

An **algorithm** is a set of step-by-step instructions for solving a problem.  
Algorithms are important because different approaches to the same problem can have very different levels of efficiency.

---

## Simple Search (Linear Search)

**Simple search** checks each element in a list one by one until the desired item is found or the list ends.

### Characteristics
- Works on any list (sorted or unsorted)
- Easy to understand and implement

### Performance
- Best case: the item is found immediately → **1 step**
- Worst case: the item is at the end or not present → **n steps**

**Time complexity:** `O(n)`

---

## Binary Search

**Binary search** is a faster search algorithm that works only on **sorted lists**.

### How It Works
1. Check the middle element of the list
2. If the middle element is the target, stop
3. If the target is smaller, repeat on the left half
4. If the target is larger, repeat on the right half
5. Continue until the element is found or the list is empty

Each step eliminates half of the remaining elements.

### Example
For a list of 128 elements:
- Step 1 → 64 elements left
- Step 2 → 32 elements left
- Step 3 → 16 elements left
- Step 4 → 8 elements left
- Step 5 → 4 elements left
- Step 6 → 2 elements left
- Step 7 → 1 element left

Maximum of **7 steps**.

### Performance
**Time complexity:** `O(log n)`

---

## Comparison: Simple Search vs Binary Search

| Search Method | Maximum Steps (n elements) |
|--------------|---------------------------|
| Simple Search | n                         |
| Binary Search | log₂ n                    |

Binary search is significantly faster for large lists.

---

## Big O Notation (Introduction)

**Big O notation** describes how the running time of an algorithm grows as the input size increases. It focuses on the **worst-case scenario**.

### Common Big O Values in This Chapter
- `O(n)` — Linear time (simple search)
- `O(log n)` — Logarithmic time (binary search)

Big O notation ignores constants and focuses on growth rate.

---

## Key Points

- Algorithms can be compared based on efficiency
- Binary search requires sorted data
- Binary search is much faster than simple search for large inputs
- Big O notation is used to describe algorithm performance
