### **What is Recursion?**

Recursion is a programming technique where a function calls itself directly or indirectly to solve a problem. Instead of using iterative loops, recursion solves a problem by breaking it down into smaller subproblems that are similar to the original problem. A recursive function works by making the problem simpler until it reaches a base case that stops the recursion.

### **Key Components of Recursion**

1. **Base Case**:
   - Every recursive function needs a base case, which is a condition where the recursion stops.
   - Without a base case, recursion would go on indefinitely, causing a stack overflow (an error due to too many function calls).
   
   Example of a base case:
   ```python
   def factorial(n):
       if n == 0:  # base case
           return 1
   ```

2. **Recursive Case**:
   - In the recursive case, the function calls itself with a simpler version of the input. Each recursive step reduces the problem size and gradually leads to the base case.
   - The recursive function should always make progress toward reaching the base case.

   Example of a recursive case:
   ```python
   def factorial(n):
       if n == 0:  # base case
           return 1
       return n * factorial(n - 1)  # recursive case
   ```

### **How Recursion Works**
The function keeps calling itself with smaller inputs until it reaches the base case. Once the base case is reached, the function stops calling itself and begins to return values back to the previous calls, unwinding the recursive calls.

#### Example of a simple recursive function (Factorial):
The factorial of a number `n` is defined as:
\[ n! = n \times (n - 1) \times (n - 2) \times \dots \times 1 \]

Recursive version:
```python
def factorial(n):
    # Base case: if n is 0, return 1
    if n == 0:
        return 1
    # Recursive case: n * factorial of (n-1)
    return n * factorial(n - 1)
```

Calling `factorial(4)` would unfold like this:
```
factorial(4) = 4 * factorial(3)
factorial(3) = 3 * factorial(2)
factorial(2) = 2 * factorial(1)
factorial(1) = 1 * factorial(0)
factorial(0) = 1 (Base Case)
```
Now, it returns the values back:
```
factorial(1) = 1
factorial(2) = 2 * 1 = 2
factorial(3) = 3 * 2 = 6
factorial(4) = 4 * 6 = 24
```
Final result: `factorial(4) = 24`

### **Key Properties of Recursion**
1. **Smaller Subproblems**: Each recursive call should simplify the problem and move toward the base case.
2. **Stack Space**: Every function call adds a new frame to the call stack. Too many recursive calls can result in a stack overflow, so care should be taken in deep recursion.
3. **Overlapping Subproblems**: In some cases, recursive solutions might compute the same subproblems multiple times, leading to inefficiency (this can be mitigated with techniques like **memoization**).

### **Recursion vs. Iteration**
- **Recursion**: Uses function calls to solve problems, often more elegant but can use more memory due to the call stack.
- **Iteration**: Uses loops to repeat a process, generally more efficient in terms of memory.

#### When to Use Recursion?
- Problems that can be naturally divided into smaller subproblems, like **tree traversal**, **sorting algorithms** (e.g., Merge Sort), **combinatorics** (e.g., factorial, Fibonacci), etc.

---

### **Examples of Recursion**

Let’s now explore the solutions for the problems you asked about, using recursion:

### 1. **Recursive Implementation of `atoi()`**

The problem is to convert a string representing an integer into the corresponding integer value using recursion.

#### Steps:
1. **Base Case**: If the string is empty, return 0.
2. **Recursive Case**: 
    - Take the last character of the string, convert it to an integer.
    - Multiply the recursive result of the remaining string by 10 and add the last digit.

#### Python Code:
```python
def recursive_atoi(s):
    # Base case: if the string is empty, return 0
    if len(s) == 0:
        return 0
    
    # Handle negative numbers
    if s[0] == '-':
        return -recursive_atoi(s[1:])
    
    # Recursive case: convert the last character and add to the result
    last_digit = ord(s[-1]) - ord('0')
    return recursive_atoi(s[:-1]) * 10 + last_digit

# Example usage
s = "1234"
print(recursive_atoi(s))  # Output: 1234
```

### 2. **`Pow(x, n)` (Calculate `x^n` using recursion)**

#### Steps:
1. **Base Case**: If `n` is 0, return 1 (since any number raised to the power of 0 is 1).
2. **Recursive Case**: 
    - If `n` is even, use the formula `pow(x, n//2) * pow(x, n//2)`.
    - If `n` is odd, use `x * pow(x, n - 1)`.

#### Python Code:
```python
def pow(x, n):
    # Base case: x^0 is 1
    if n == 0:
        return 1
    # If n is negative, calculate the positive power and take reciprocal
    if n < 0:
        return 1 / pow(x, -n)
    # If n is even
    elif n % 2 == 0:
        half = pow(x, n // 2)
        return half * half
    # If n is odd
    else:
        return x * pow(x, n - 1)

# Example usage
x, n = 2.0, 10
print(pow(x, n))  # Output: 1024.0
```

### 3. **Count Good Numbers**

We can assume that good numbers follow a rule where even indices must have even digits and odd indices must have prime digits (2, 3, 5, 7).

#### Steps:
1. **Recursive Case**:
    - For each index, determine the valid digit set (even digits for even indices, prime digits for odd indices).
    - Recursively count for the rest of the string.
2. **Base Case**: When the index reaches `n`, stop recursion.

#### Python Code:
```python
def count_good_numbers(n):
    MOD = 10**9 + 7
    
    def helper(index):
        if index == n:
            return 1
        if index % 2 == 0:
            return (5 * helper(index + 1)) % MOD  # 5 even digits
        else:
            return (4 * helper(index + 1)) % MOD  # 4 prime digits

    return helper(0)

# Example usage
n = 4
print(count_good_numbers(n))  # Output: 400
```

### 4. **Sort a Stack Using Recursion**

#### Steps:
1. **Base Case**: If the stack is empty, return.
2. **Recursive Case**:
    - Pop the top element.
    - Sort the remaining stack recursively.
    - Insert the popped element in its correct position.

#### Python Code:
```python
def sort_stack(stack):
    # Base case: empty stack
    if len(stack) == 0:
        return
    
    # Pop the top element
    top = stack.pop()
    
    # Sort the remaining stack recursively
    sort_stack(stack)
    
    # Insert the popped element in the sorted order
    insert_in_sorted_order(stack, top)

def insert_in_sorted_order(stack, element):
    if len(stack) == 0 or stack[-1] <= element:
        stack.append(element)
    else:
        top = stack.pop()
        insert_in_sorted_order(stack, element)
        stack.append(top)

# Example usage
stack = [3, 1, 4, 2]
sort_stack(stack)
print(stack)  # Output: [1, 2, 3, 4]
```

### 5. **Reverse a Stack Using Recursion**

#### Steps:
1. **Base Case**: If the stack is empty, return.
2. **Recursive Case**:
    - Pop the top element.
    - Reverse the remaining stack recursively.
    - Insert the popped element at the bottom of the reversed stack.

#### Python Code:
```python
def reverse_stack(stack):
    # Base case: empty stack
    if len(stack) == 0:
        return
    
    # Pop the top element
    top = stack.pop()
    
    # Reverse the remaining stack
    reverse_stack(stack)
    
    # Insert the popped element at the bottom
    insert_at_bottom(stack, top)

def insert_at_bottom(stack, element):
    if len(stack) == 0:
        stack.append(element)
    else:
        top = stack.pop()
        insert_at_bottom(stack, element)
        stack.append(top)

# Example usage
stack = [1, 2, 3, 4]
reverse_stack(stack)
print(stack)  # Output

: [4, 3, 2, 1]
```

---

Recursion is a powerful technique for solving problems where the solution can be broken down into simpler, self-similar subproblems, but it needs to be used with caution to avoid inefficiency and stack overflow issues.