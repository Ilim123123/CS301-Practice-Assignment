# CS 301: Design and Analysis of Algorithms
## Practice Assignment

---

## Task 1. Recursive Fibonacci

### Python Code
```python
def fibonacci(n):
    if n <= 0:
        return 0
    elif n == 1:
        return 1
    return fibonacci(n - 1) + fibonacci(n - 2)
```

### Examples and Call Trees

#### Example 1: `fibonacci(3)`
```text
       fib(3) -> 2
      /      \
  fib(2)->1  fib(1)->1
  /     \
fib(1)->1 fib(0)->0
```
**Explanation:** `fib(3)` calls `fib(2)` and `fib(1)`. `fib(2)` calls `fib(1)` and `fib(0)`. Total result = 1 + 1 = 2.

#### Example 2: `fibonacci(4)`
```text
            fib(4) -> 3
          /            \
      fib(3)->2        fib(2)->1
     /        \        /       \
  fib(2)->1  fib(1)  fib(1)   fib(0)
  /     \      |       |        |
fib(1) fib(0)  1       1        0
```
**Explanation:** `fib(4)` calls `fib(3)` (returns 2) and `fib(2)` (returns 1). Result = 3.

#### Example 3: `fibonacci(5)`
```text
                  fib(5) -> 5
               /              \
         fib(4)->3           fib(3)->2
        /        \          /        \
    fib(3)      fib(2)    fib(2)    fib(1)
   /     \      /   \     /   \       |
fib(2) fib(1) fib(1)fib(0)fib(1)fib(0) 1
```
**Explanation:** `fib(5)` aggregates the outputs of `fib(4)` (3) and `fib(3)` (2) to return 5.

---

## Task 2. Iterative Binary Search

### Python Code
```python
def binary_search_iterative(arr, target):
    left = 0
    right = len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
            
    return -1
```

### Examples & Step-by-step Progress

#### Example 1: Search `7` in `[1, 3, 5, 7, 9, 11]`
* **Iteration 1:** `left = 0`, `right = 5`, `mid = 2` (`arr[2] = 5`). Since $5 < 7$, search moves to right half: `left = 3`.
* **Iteration 2:** `left = 3`, `right = 5`, `mid = 4` (`arr[4] = 9`). Since $9 > 7$, search moves to left half: `right = 3`.
* **Iteration 3:** `left = 3`, `right = 3`, `mid = 3` (`arr[3] = 7`). Target found at index `3`.

#### Example 2: Search `2` in `[2, 4, 6, 8, 10]`
* **Iteration 1:** `left = 0`, `right = 4`, `mid = 2` (`arr[2] = 6`). Since $6 > 2$, `right = 1`.
* **Iteration 2:** `left = 0`, `right = 1`, `mid = 0` (`arr[0] = 2`). Target found at index `0`.

#### Example 3: Search `12` (not present) in `[10, 20, 30, 40]`
* **Iteration 1:** `left = 0`, `right = 3`, `mid = 1` (`arr[1] = 20`). Since $20 > 12$, `right = 0`.
* **Iteration 2:** `left = 0`, `right = 0`, `mid = 0` (`arr[0] = 10`). Since $10 < 12$, `left = 1`.
* **End:** `left > right` (1 > 0), returns `-1`.

---

## Task 3. Recursive Binary Search

### Python Code
```python
def binary_search_recursive(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1
        
    if left > right:
        return -1
        
    mid = (left + right) // 2
    
    if arr[mid] == target:
        return mid
    elif arr[mid] > target:
        return binary_search_recursive(arr, target, left, mid - 1)
    else:
        return binary_search_recursive(arr, target, mid + 1, right)
```
