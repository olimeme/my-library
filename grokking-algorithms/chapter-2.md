# Chapter 2

## Selection Sort

**Selection sort** is a simple sorting algorithm that repeatedly finds the smallest element in a list and adds it to a new sorted list.

---

## How Selection Sort Works

1. Find the smallest element in the list
2. Remove it from the list
3. Add it to the new sorted list
4. Repeat until the original list is empty

At the end, the new list contains all elements in sorted order.

---

## Finding the Smallest Element

To find the smallest element:
- Start by assuming the first element is the smallest
- Compare it with every other element
- Update the smallest value whenever a smaller element is found

This process requires checking **every element** in the list.

---

## Algorithm Steps (Conceptual)

- Input: Unsorted list
- Output: Sorted list
- Repeatedly scan the list to find the smallest remaining item
- Move that item to the sorted list

---

## Time Complexity Analysis

### Comparisons
- First pass: n comparisons
- Second pass: n − 1 comparisons
- Third pass: n − 2 comparisons
- …
- Total comparisons ≈ n × n / 2

### Big O Notation
- **Time complexity:** `O(n²)`
- Applies even in the best case

Selection sort does not get faster with partially sorted data.

---

## Space Complexity

- Requires additional space for the new list
- **Space complexity:** `O(n)`

---

## Characteristics of Selection Sort

- Simple to understand and implement
- Inefficient for large datasets
- Always performs the same number of comparisons
- Useful mainly for learning and teaching purposes

---

## Big O Takeaway

- `O(n²)` algorithms become very slow as input size grows
- Even with fast computers, inefficient algorithms do not scale well