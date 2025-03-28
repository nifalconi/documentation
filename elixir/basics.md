# Elixir Day-to-Day Cheat Sheet

This quick reference mirrors the style of a Python cheat sheet but focuses on Elixir basics. It includes fundamental operations, key modules, and a special spotlight on **pattern matching**—one of Elixir’s most powerful features.

## Table of Contents
1. [Strings](#strings)
2. [Lists](#lists)
3. [Tuples](#tuples)
4. [Maps](#maps)
5. [Pattern Matching](#pattern-matching)
    - [Why It’s Powerful](#why-its-powerful)
    - [Examples](#examples)
    - [Filter with Pattern Matching](#filter-with-pattern-matching)
6. [Pipes (|>)](#pipes-)
7. [Day-to-Day Elixir Tips](#day-to-day-elixir-tips)

---

## Strings

Elixir provides the `String` module for most string operations. Strings are **immutable** binaries under the hood, so every “modification” returns a new string.

### Stripping and Case Conversion

```elixir
s = "  Hello, World!  "

String.trim(s)          # "Hello, World!" - Remove whitespace from both ends
String.trim_leading(s)  # "Hello, World!  " - Remove whitespace from the start
String.trim_trailing(s) # "  Hello, World!" - Remove whitespace from the end

String.downcase(s)      # "  hello, world!  "
String.upcase(s)        # "  HELLO, WORLD!  "
String.capitalize(s)    # "  hello, world!  " - All but first letter lowercased
```

### Checking Substring & Other Inspections

```elixir
String.contains?(s, "World")    # true
String.contains?(s, "Python")   # false

String.starts_with?(s, "  He")  # true
String.ends_with?(s, "!  ")     # true

String.length(s)                # 17 (spaces count too)
```

### Finding and Replacing

```elixir
String.replace(s, "World", "Elixir")
# "  Hello, Elixir!  "

String.replace(s, "l", "X", global: false)
# "  HeXlo, World!  " (replaces first occurrence only)

String.slice(s, 2..6)   # "Hello" (using a Range)
String.slice(s, 2, 5)   # "Hello" (start index 2, length 5)

String.index(s, "World")
# 9 (zero-based), or nil if not found
```

### Splitting and Joining

```elixir
String.split(s)
# ["Hello,", "World!"] - split by whitespace

String.split(s, ",")
# ["  Hello", " World!  "] - split by delimiter

String.split(s, ~r/\W+/)
# ["", "Hello", "World", ""] - Regex-based split on non-word chars

String.join(["Hello", "Elixir"], " ")
# "Hello Elixir"
```

### Interpolation

```elixir
name = "Alice"
"Hello, #{name}!"
# "Hello, Alice!"
```

---

## Lists

Elixir’s lists are **linked lists**. For large data handling, you might prefer `Enum` or `Stream`.

```elixir
lst = [1, 2, 3, 4]
```

### Adding, Removing, and Combining Elements

```elixir
# Prepend (efficient):
new_list = [0 | lst]
# [0, 1, 2, 3, 4]

# Concatenate
combined = lst ++ [5, 6]
# [1, 2, 3, 4, 5, 6]

# Subtract
less = combined -- [3]
# [1, 2, 4, 5, 6]

# Head / Tail
hd(lst)  # 1
tl(lst)  # [2, 3, 4]
```

### Querying

```elixir
length(lst)                # 4
Enum.member?(lst, 2)       # true
Enum.count(lst, &(&1 > 2)) # 2 (counts 3 and 4)

Enum.at(lst, 1)            # 2
```

### Mapping, Filtering, Reducing

```elixir
Enum.map(lst, fn x -> x * 2 end)
# [2, 4, 6, 8]

Enum.filter(lst, fn x -> rem(x, 2) == 0 end)
# [2, 4]

Enum.reduce(lst, 0, fn x, acc -> x + acc end)
# 10 (sum)
```

### Sorting and Reversing

```elixir
Enum.sort([3, 1, 2])
# [1, 2, 3]

Enum.sort_by(["apple", "banana", "pear"], &String.length/1)
# ["pear", "apple", "banana"]

Enum.reverse(lst)
# [4, 3, 2, 1]
```

### Slicing and Chunking

```elixir
Enum.slice(lst, 1, 2)
# [2, 3]

Enum.chunk_every(lst, 2)
# [[1, 2], [3, 4]]

List.first(lst)  # 1
List.last(lst)   # 4
```

### Removing Duplicates

```elixir
dupes = [1, 2, 2, 3, 1, 4]
Enum.uniq(dupes)
# [1, 2, 3, 4]
```

### Flattening Nested Lists

```elixir
nested = [[1, 2], [3, 4, [5]], 6]
List.flatten(nested)
# [1, 2, 3, 4, 5, 6]
```

### Zipping

```elixir
letters = [:a, :b, :c]
numbers = [1, 2, 3]
Enum.zip(letters, numbers)
# [a: 1, b: 2, c: 3]
```

---

## Tuples

Tuples in Elixir are stored contiguously in memory. They’re great for small, fixed data.

```elixir
tup = {:ok, "Something happened"}

elem(tup, 0)            # :ok
elem(tup, 1)            # "Something happened"
put_elem(tup, 1, "New") # {:ok, "New"} (returns a new tuple)
```

---

## Maps

Elixir’s main key-value store. Keys can be atoms, strings, numbers, etc.

```elixir
my_map = %{name: "Alice", age: 30, city: "New York"}

my_map.name         # "Alice"
my_map[:age]        # 30

Map.get(my_map, :city)          # "New York"
Map.fetch(my_map, :city)        # {:ok, "New York"}
Map.fetch(my_map, :bad_key)     # :error

new_map = Map.put(my_map, :age, 31)
# %{name: "Alice", age: 31, city: "New York"}
```

---

## Pattern Matching

Pattern matching is a core feature in Elixir that lets you match structures, assign values to variables, and control flow via matches. This is **not** just simple tuple/list unpacking—it involves asserting the “shape” of your data.

### Why It’s Powerful

1. **Cleaner Control Flow**  
   Instead of writing a lot of `if/else` logic, you can match on data shapes.

2. **Multiple Function Heads**  
   Functions can have multiple definitions, each handling a specific pattern.

3. **Expressiveness**  
   You explicitly describe the shape of data, making code very declarative.

### Examples

```elixir
{status, message} = {:ok, "Hello!"}
# status = :ok, message = "Hello!"

{status, message} = {:error, "Oops"}
# status = :error, message = "Oops"

# If it doesn't match, a MatchError is raised:
{status, message} = {:ok, "Hello!", 123}
# ** (MatchError) no match of right hand side value: {:ok, "Hello!", 123}
```

#### Pattern Matching in Function Heads

```elixir
defmodule Greeter do
  def greet({first, last}) do
    "Hello, #{first} #{last}"
  end

  def greet(:anonymous) do
    "Hello, mysterious stranger!"
  end
end

Greeter.greet({"Alice", "Smith"})
# "Hello, Alice Smith"

Greeter.greet(:anonymous)
# "Hello, mysterious stranger!"
```

#### Using `case` with Pattern Matching

```elixir
case {:ok, "User created"} do
  {:ok, msg} ->
    "Success: #{msg}"

  {:error, reason} ->
    "Failed: #{reason}"

  _ ->
    "Unknown response"
end
```

#### Pattern Matching with Lists

```elixir
[head | tail] = [1, 2, 3, 4]
head  # 1
tail  # [2, 3, 4]

# Matching specific shapes
[1, 2, x] = [1, 2, 3]
x  # 3
```

### Filter with Pattern Matching

You can use pattern matching **inside** `Enum.filter/2` (or list comprehensions) to select data in a concise way:

```elixir
responses = [
  {:ok, "Success!"},
  {:error, "Bad request"},
  {:ok, "Data saved"},
  {:error, "Server error"},
  {:ok, "All good"}
]

ok_responses = Enum.filter(responses, fn
  {:ok, _msg} -> true
  _ -> false
end)

# ok_responses == [
#   {:ok, "Success!"},
#   {:ok, "Data saved"},
#   {:ok, "All good"}
# ]
```

---

## Pipes (|>)

The pipe operator (`|>`) passes the result of one expression as the first argument to the next function:

```elixir
"  hello elixir  "
|> String.trim()
|> String.upcase()
|> String.replace("ELIXIR", "WORLD")
# "HELLO WORLD"
```

---

## Day-to-Day Elixir Tips

1. **IEx is your friend**  
   - `iex` for the interactive shell  
   - `h String.split` or `h Enum.map` for inline docs  

2. **Everything is Immutable**  
   - Variables can be rebound but not mutated in place  

3. **Leverage `Enum`**  
   - Most list-like operations live in the `Enum` module (also works on other enumerables)  

4. **Use pattern matching for clean code**  
   - Function heads, `case` statements, and direct assignments  

5. **Embrace OTP and concurrency**  
   - For bigger projects, you’ll use processes, supervisors, and message passing  

6. **Let it Crash**  
   - Don’t fear processes crashing; OTP is designed to handle restarts gracefully  

---

**Happy coding in Elixir!**
