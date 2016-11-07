
**Creating a `map` function**

```elixir
def map([], _func), do: []
def map([ head | tail ], func), do: [func.(head) | map(tail, func)]
```
Replace **func** above with your function like below:

```elixir
iex> MyList.map [1,2,3,4], fn (n) -> n*n end
[1, 4, 9, 16]
```

**Keeping Track of Values During Recursion**
Pass the state in a function's parameter:

```elixir
defmodule MyList do
  def sum([], total), do: total
  def sum([ head | tail ], total), do: sum(tail, head+total)
end
```
In the above example, you'll generally initialize `total` with a value of `0`.

**`reduce`, baby!**

```elixir
defmodule MyList do
  def reduce([], value, _) do
    value
  end
  def reduce([ head | tail ], value, func) do
    reduce(tail, func.(head, value), func)
  end
end
```

**Keyword Lists**
ex. `@defaults [fg: "black", bg: "white", font: "Merriweather"]`
for access: `kwlist[key]`

**Maps**
ex. `%{ name: "Dave", likes: "Programming", where: "Dallas" }`
