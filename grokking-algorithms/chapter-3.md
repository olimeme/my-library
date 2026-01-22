# Chapter 3

## Recursion

**Recursion** is a programming technique where a function calls itself to solve a problem.  
Each recursive function has two essential parts:
- A **base case** that stops the recursion
- A **recursive case** that reduces the problem

---

## Base Case and Recursive Case

### Base Case
The condition under which the function stops calling itself.  
Without a base case, recursion would continue forever.

### Recursive Case
The part of the function where it calls itself with a smaller or simpler input.

Both cases are required for recursion to work correctly.

---

## How the Call Stack Works

When a function is called, it is added to the **call stack**.  
The call stack keeps track of:
- Which function is currently running
- What function needs to resume after the current one finishes

Each recursive call adds a new frame to the call stack.

---

## Stack Overflow

If recursion goes too deep or has no base case:
- The call stack grows too large
- The program runs out of memory
- This causes a **stack overflow**

Proper base cases prevent this problem.

---

## Recursion vs Loops

Many problems solved with loops can also be solved with recursion.

### Loops
- Use iteration
- Generally use less memory
- Easier to debug for simple tasks

### Recursion
- Can make code cleaner and more readable
- Useful for problems that can be divided into smaller subproblems
- Uses more memory due to the call stack

---

## Example Problems Suitable for Recursion

- Counting down numbers
- Factorials
- Traversing directories
- Divide-and-conquer algorithms

Recursion works best when a problem can be broken into **similar subproblems**.