# Python Basics

This document exists due to my complete lack of good memory.

## Strings

### Stripping and Case Conversion
```python
s = "  Hello, World!  "
s.strip()      # "Hello, World!" - Remove spaces from both sides
s.lstrip()     # "Hello, World!  " - Remove spaces from the left
s.rstrip()     # "  Hello, World!" - Remove spaces from the right
s.lower()      # "  hello, world!  " - Convert to lowercase
s.upper()      # "  HELLO, WORLD!  " - Convert to uppercase
s.capitalize() # "  hello, world!  " - Capitalize the first letter
s.title()      # "  Hello, World!  " - Title-case each word
```

### Padding
```python
s.center(20, "*")   # "****Hello, World!****" - Center align with padding
s.ljust(20, "-")    # "Hello, World!-------" - Left align with padding
s.rjust(20, "=")    # "=======Hello, World!" - Right align with padding
s.zfill(20)         # "0000   Hello, World!   " - Pad with zeros to the left
```

### Substring Checking
```python
"World" in s        # True - Check if "World" exists in the string
"Python" not in s   # True - Check if "Python" does not exist in the string
```

### Finding and Replacing
```python
s.find("World")    # 9 - Index of first occurrence, or -1 if not found
s.rfind("o")       # 8 - Index of last occurrence
s.replace("World", "Python")  # "  Hello, Python!  " - Replace all occurrences
s.count("o")       # 2 - Count occurrences of a substring
```

### Validation
```python
s.isdigit()    # False - Check if all characters are digits
s.isalpha()    # False - Check if all characters are alphabetic
s.isalnum()    # False - Check if all characters are alphanumeric
s.isspace()    # False - Check if all characters are whitespace
```

### Splitting and Joining
```python
s.split()             # ['Hello,', 'World!'] - Split by whitespace
s.split(",")          # ['  Hello', ' World!  '] - Split by a delimiter
".".join(["A", "B"])  # "A.B" - Join list elements with a delimiter
```

### Checking Start/End
```python
s.startswith("  He")  # True - Check if string starts with substring
s.endswith("!  ")     # True - Check if string ends with substring
```

### Other String Operations
```python
len(s)               # 13 - Get the length of the string
s[::-1]              # "!dlroW ,olleH" - Reverse a string
"".join(reversed(s)) # "!dlroW ,olleH" - Reverse using `reversed`
```

---

## Lists

### Adding and Removing Elements
```python
lst = [1, 2, 3, 4]
lst.append(5)         # [1, 2, 3, 4, 5] - Add an element to the end
lst.insert(1, 9)      # [1, 9, 2, 3, 4] - Insert 9 at index 1
lst.pop()             # 4 - Remove and return the last element
lst.pop(1)            # 9 - Remove and return element at index 1
lst.remove(2)         # [1, 3, 4] - Remove the first occurrence of 2
lst.clear()           # [] - Remove all elements
```

### Querying
```python
len(lst)              # 4 - Get the length of the list
lst.index(3)          # 2 - Index of the first occurrence of 3
lst.count(3)          # 1 - Count occurrences of 3
```

### Sorting and Reversing
```python
lst.sort()            # [1, 2, 3, 4] - Sort the list in ascending order
lst.sort(reverse=True) # [4, 3, 2, 1] - Sort in descending order
sorted(lst)           # [1, 2, 3, 4] - Return a sorted copy
lst.reverse()         # [4, 3, 2, 1] - Reverse the list in-place
lst[::-1]             # [1, 2, 3, 4] - Return a reversed copy
```

### Slicing
```python
lst[1:3]              # [2, 3] - Get elements from index 1 to 2
lst[:2]               # [1, 2] - Get first two elements
lst[2:]               # [3, 4] - Get elements from index 2 to the end
lst[::2]             # [1, 3] - Get every second element
lst[::-1]            # [4, 3, 2, 1] - Get reversed list
lst[1:4:2]           # [2, 4] - Slice with a step of 2
```

### Copying
```python
lst.copy()            # Create a shallow copy
lst[:]                # Create a shallow copy using slicing
list(lst)            # Create a copy using list()
```

### Combining and Extending
```python
lst.extend([5, 6])    # [1, 2, 3, 4, 5, 6] - Add all elements of another list
lst + [7, 8]          # [1, 2, 3, 4, 7, 8] - Concatenate lists
```

### Miscellaneous
```python
any(lst)             # True - Check if any element is truthy
all(lst)             # True - Check if all elements are truthy
max(lst)             # 4 - Get the largest value
min(lst)             # 1 - Get the smallest value
sum(lst)             # 12 - Get the sum of all elements
```

---

## Advanced Tricks

### Enumerate
```python
lst = ["a", "b", "c"]
for index, value in enumerate(lst):
    print(index, value)
# 0 a
# 1 b
# 2 c
```

### Zip
```python
keys = ["name", "age", "city"]
values = ["Alice", 30, "New York"]
zipped = zip(keys, values)
print(list(zipped))  # [("name", "Alice"), ("age", 30), ("city", "New York")]
```

### Flattening Nested Lists
```python
nested = [[1, 2], [3, 4], [5]]
flat = [x for sublist in nested for x in sublist]
print(flat)  # [1, 2, 3, 4, 5]
```

### Removing Duplicates While Preserving Order
```python
lst = [1, 2, 2, 3, 4, 3]
deduplicated = list(dict.fromkeys(lst))
print(deduplicated)  # [1, 2, 3, 4]
```

### Transposing a Matrix
```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
transposed = [list(row) for row in zip(*matrix)]
print(transposed)  # [[1, 4, 7], [2, 5, 8], [3, 6, 9]]
```

### Cartesian Product
```python
lst1 = [1, 2]
lst2 = ["a", "b"]
product = [(x, y) for x in lst1 for y in lst2]
print(product)  # [(1, "a"), (1, "b"), (2, "a"), (2, "b")]
```


Updated 2025
