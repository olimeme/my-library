# Chapter 4

## Quicksort and Divide & Conquer

---

## 1. Divide and Conquer (D&C)
D&C is a recursive technique for solving problems. It’s not just an algorithm you run; it's a way of thinking about problem-solving.

### The D&C Strategy:
1.  **Identify the Base Case:** This must be the simplest possible version of the problem.
2.  **Divide/Reduce:** Figure out how to reduce your problem until it becomes the base case.

### Example: The Farm Plot Problem
Imagine a farmer has a rectangular plot (e.g., 1680m x 640m) and wants to divide it into the largest possible equal square plots.
* Instead of guessing, you use the **Euclidean Algorithm**. 
* You fit the largest squares possible into the rectangle.
* You apply the same logic to the remaining smaller rectangle.
* **The Base Case:** When one side is a multiple of the other (e.g., 160m x 80m), you've found the largest square size.



---

## 2. Quicksort
Quicksort uses D&C to sort an array. It is significantly faster than Selection Sort.

### The Process:
1.  **Pick a Pivot:** Choose an element from the array (e.g., the first element, the last, or a random one).
2.  **Partitioning:** Separate the remaining elements into two sub-arrays:
    * **Left:** Elements smaller than the pivot.
    * **Right:** Elements larger than the pivot.
3.  **Recurse:** Call Quicksort on the left and right sub-arrays.

### The Base Case:
An array is "sorted" if it has 0 or 1 elements. Recursion stops here.



---

## 3. Big O Notation: Average vs. Worst Case
Quicksort is unique because its performance depends on the **pivot** choice.

| Scenario | Big O | Cause |
| :--- | :--- | :--- |
| **Worst Case** | $O(n^2)$ | The pivot is always the smallest or largest element (creates a "tall" stack). |
| **Average Case** | $O(n \log n)$ | The pivot is near the middle (creates a "short/balanced" stack). |

### Why O(n log n)?
* **The height of the stack** is $O(\log n)$ (the number of times you split the array).
* **The width of each level** is $O(n)$ (each level requires looking at all elements once).
* Total time: **Height × Width** = $O(n \log n)$.

---

## 4. Key Takeaways
* **Recursion** is the engine behind D&C.
* **Functional Programming:** D&C is often easier to implement in functional languages.
* **Randomization:** To ensure you hit the $O(n \log n)$ average case, always pick a **random element** as the pivot.
* **Inductive Proofs:** A way to prove your algorithm works. If it works for the base case and the case $n+1$, it works for all cases.

---
> **Recursive Tip:** When you see a problem like "Sum the numbers in an array," don't think of a loop. Think: `Sum([1, 2, 3])` is just `1 + Sum([2, 3])`.