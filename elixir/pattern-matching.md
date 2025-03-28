# Elixir Pattern Matching Guide

Pattern matching is **one of the most powerful features** in Elixir—and at the heart of how the language works. It goes far beyond basic variable assignment. Once you learn to use it, you’ll find yourself writing clearer, shorter, and more expressive code.

This guide will walk you through the most common (and useful) pattern matching scenarios.

---

## 🔄 Basic Assignment

In Elixir, the `=` operator doesn't mean "assign"—it means "match".

```elixir
x = 1
# x is bound to 1

1 = 1
# ✅ Match succeeds

1 = 2
# ❌ MatchError: no match of right hand side value: 2
```

---

## 📦 Matching Tuples

You can destructure tuples directly:

```elixir
{:ok, result} = {:ok, 42}
# result = 42

{:error, _reason} = {:error, "Something went wrong"}
# Matches and ignores the second element using `_`
```

This is especially common in return values from functions like `File.read/1`, `Map.fetch/2`, etc.

---

## 📝 Matching Lists

```elixir
[head | tail] = [1, 2, 3]
# head = 1
# tail = [2, 3]

[1, 2, 3] = [1, 2, 3]
# ✅ full list match

[1, _x, 3] = [1, 5, 3]
# _x = 5
```

You can use `_` to ignore values you don't care about.

---

## 🔍 Matching with Pin Operator (^)

By default, variables in patterns get rebound:

```elixir
x = 1
x = 2  # x is now 2
```

But sometimes you want to **match against a previously bound value**, not rebind it. That’s what `^` is for:

```elixir
x = 1
^x = 1  # ✅ match succeeds
^x = 2  # ❌ MatchError
```

---

## 💡 Pattern Matching in `case`

```elixir
case {:ok, "Elixir"} do
  {:ok, value} ->
    "Success: #{value}"

  {:error, reason} ->
    "Error: #{reason}"

  _ ->
    "Unknown result"
end
```

This is more elegant than `if`/`else` chains and scales better for multiple conditions.

---

## 🧠 Matching in Function Definitions

Elixir lets you define multiple versions of a function based on input shape:

```elixir
defmodule Greeter do
  def greet({first, last}) do
    "Hello, #{first} #{last}"
  end

  def greet(:guest) do
    "Hello, stranger!"
  end
end
```

It will automatically call the function clause that matches the input.

---

## 🎯 Matching Maps

You can match on specific keys in a map:

```elixir
%{name: name} = %{name: "Alice", age: 30}
# name = "Alice"

%{age: 30} = %{name: "Bob", age: 30}
# ✅ matches because :age is present and equals 30

%{height: _} = %{name: "Eve"}
# ❌ MatchError: key :height not found
```

Use `Map.get/2` if you want to avoid crashes for missing keys.

---

## 🧪 Pattern Matching in `with`

Use `with` when you want to chain multiple pattern matches elegantly:

```elixir
with {:ok, user} <- fetch_user(id),
     {:ok, plan} <- fetch_plan(user),
     do: {:ok, %{user: user, plan: plan}}

# If any step returns {:error, reason}, it short-circuits
```

---

## 🔥 Bonus: Filtering with Pattern Matching

You can use pattern matching inside `Enum.filter`:

```elixir
responses = [
  {:ok, "Done"},
  {:error, "Oops"},
  {:ok, "Saved"},
  {:error, "Timeout"}
]

Enum.filter(responses, fn
  {:ok, _} -> true
  _ -> false
end)

# => [{:ok, "Done"}, {:ok, "Saved"}]
```

## 🧱 Matching Lists (Advanced)

### Match a fixed-size list

```elixir
[1, 2, 3] = [1, 2, 3]
# ✅ Matches

[1, 2, 3] = [1, 2]
# ❌ MatchError
```

### Match with `|` operator

```elixir
[head | tail] = [10, 20, 30, 40]
# head = 10
# tail = [20, 30, 40]
```

### Nested head-tail pattern

```elixir
[[a | b] | rest] = [[1, 2, 3], [4, 5]]
# a = 1
# b = [2, 3]
# rest = [[4, 5]]
```

### Match and ignore certain values

```elixir
[_, second, _] = [1, 99, 3]
# second = 99
```

## 🧱 Matching Maps and Structs

### Match on specific keys

```elixir
person = %{name: "Nico", age: 31, city: "Santiago"}

%{name: name} = person
# name = "Nico"

%{age: 31} = person
# ✅ Matches

%{height: _} = person
# ❌ MatchError (key :height not present)
```

### Match nested maps

```elixir
data = %{user: %{name: "Ana", email: "ana@example.com"}}

%{user: %{name: name}} = data
# name = "Ana"
```

### Match structs

```elixir
defmodule User do
  defstruct [:id, :name]
end

user = %User{id: 1, name: "Lucas"}

%User{name: name} = user
# name = "Lucas"

%User{id: ^id} = %User{id: 1, name: "Nico"}
# works if `id` is already bound and equal
```

### Guard clauses with structs

```elixir
defmodule Order do
  defstruct [:total]
end

defmodule Matcher do
  def is_big_order(%Order{total: t}) when t > 1000, do: :yes
  def is_big_order(_), do: :no
end

Matcher.is_big_order(%Order{total: 1200})
# :yes

Matcher.is_big_order(%Order{total: 200})
# :no
```

---

## 🎯 Complex Case Example

```elixir
case {:user, %{name: "John", roles: [:admin, :editor]}} do
  {:user, %{roles: roles}} when :admin in roles ->
    "Has admin access"

  {:user, %{roles: roles}} when :editor in roles ->
    "Has editor access"

  _ ->
    "No access"
end

# Output: "Has admin access"
```

---

## 💥 Matching in `with` with Deep Nesting

```elixir
with {:ok, %{data: %{user: %{id: id}}}} <- get_response(),
     true <- id > 0 do
  {:ok, id}
else
  _ -> :error
end
```

You can match deeply nested shapes inline!

---

## 🧰 Matching with the Pin Operator (`^`)

```elixir
expected = 42

case {:ok, 42} do
  {:ok, ^expected} -> "Matched expected!"
  _ -> "Nope"
end
```

If you don’t use `^`, `expected` would just be rebound.

---

## 🔍 Matching in Filters or Comprehensions

```elixir
people = [
  %{name: "Alice", role: :admin},
  %{name: "Bob", role: :user},
  %{name: "Carol", role: :admin}
]

admins = for %{role: :admin} = person <- people, do: person

# => [%{name: "Alice", role: :admin}, %{name: "Carol", role: :admin}]
```

You can filter directly by structure inside a list comprehension.


---

## 🧘 Recap

✅ You can pattern match on:

## 📦 Pattern Matching Summary

| Type       | Example                              | Notes                             |
|------------|--------------------------------------|-----------------------------------|
| Tuple      | `{a, b} = {1, 2}`                    | Matches elements by position      |
| List       | `[h | t] = [1,2,3]`                  | Head-tail pattern                 |
| Map        | `%{key: val} = %{key: 1}`            | Matches on key presence/value     |
| Struct     | `%User{name: n}`                     | Must match the struct type        |
| Pin        | `^var = value`                       | Matches against existing binding  |
| Guards     | `when x > 0`                         | Add conditional logic to matches  |
| Case       | `case input do ... end`              | Clean branching with shape checks |
| With       | `with {:ok, val} <- call()`          | Linear flow with fallback         |


## 🧠 Final Thoughts

Pattern matching isn't just a feature in Elixir—it's a **core mindset**. It helps you write code that's:

- More **declarative**
- More **concise**
- Easier to **reason about**


---

## 🧙 Final Words

Pattern matching may feel weird at first—especially if you're used to traditional assignment in other languages. But once it clicks, it becomes one of the most powerful tools in your Elixir toolbox.

It leads to:
- Cleaner code
- Fewer `if` statements
- More readable logic
- Easier debugging

Once you get it, you won't want to write code without it.
