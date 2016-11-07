1. [Pattern Matching](#pattern-matching)
2. [Pin Operator](#pin-operator)
3. [List](#list)
4. [Module Syntax](#module-syntax)
5. [Types](#types)
6. [Difference Between Keyword Lists and Maps](#difference-between-keyword-lists-and-maps)
7. [Join Operators](#join-operators)
8. [In Operator](#in-operator)
9. [Anonymous Functions](#anonymous-functions)
10. [Passing Functions](#passing-functions)
11. [& Notation](#&-notation)
12. [Functions within a Module](#functions-within-a-module)
13. [Clauses](#clauses)
14. [Guard clauses](#guard-clauses)
15. [Default parameters](#default-parameters)
16. [Private Functions](#private-functions)
17. [Pipe Operator](#pipe-operator)
18. [Module attributes](#module-attributes)

# Pattern Matching

```elixir
iex>list = [1, 2, 3]
[1, 2, 3]
iex>[a, 2, b ] = list
[1, 2, 3]
iex>a
1
iex>b
3
```

Underscore (\_) will be ignored — can be freely re-assigned
```elixir
iex>[1, _, _] = [1, 2, 3]
[1, 2, 3]
iex>[1, _, _] = [1, "cat", "dog"]
[1, "cat", "dog"]
```

# Pin operator

(^)

```elixir
iex>a = 1
1
iex>a = 2
2
iex>^a = 1
**(MatchError) no match of right hand side value: 1
```

# List

[ head | tail  ]

```elixir
iex> list1 = [ 3, 2, 1  ]
[3, 2, 1]
iex> list2 = [ 4 | list1  ]
[4, 3, 2, 1]
```

# Module Syntax

Module.function(parameter)

ex. `String.capitalize name`

# Types

1. Value
  * Arbitrary-sized integers: decimal (`1234`), hexadecimal (`0xcafe`), octal (`0o765`), and binary (`0b1010`) — also with underscores (`1_000_000`)
  * Floating-point numbers: `1.0`, `0.2456`, `0.314159e1`, and `314159.0e-5`
  * Atoms: `:fred`, `:is_binary?`, `:var@2`, `:<>`, `:===`, `:"func/3”`, and `:"long john silver"`
  * Ranges: `start..end` (`1..5`, `123..156`)
  * Regular expressions: Look it up, but remember to use the Regex module

2. System
  * PIDs and ports: PID is reference to a local or remote process and port is reference to a resource that you’ll be reading or writing.
  * References: Ignore for now.

3. Collection
  * Tuples: Ordered collection of values, usually only 2 to 4 per tuple (`{ 1, 2  }`, `{ :ok, 42, "next”  }`, `{ :error, :enoent  }`)
  * Lists: a linked data structure, cheap to get the head and extract the tail (but not to access in random order), see above for example
  * Keyword Lists: Elixir converts key/value pairs in a list into tuples (`[ name: "Dave", city: "Dallas", likes: "Programming”  ]` becomes `[ {:name, "Dave"}, {:city, "Dallas"}, {:likes, "Programming"}  ]`)
  * Maps: a collection of key/value pairs (`%{ key => value, key => value  }`, `%{ { :error, :enoent  } => :fatal`, `{ :error, :busy  } => :retry  }`)
  * Accessing a map: Like a Ruby hash. Also, if the keys are atoms (`:key`), you can use dot notation (`var.key`).

```elixir
iex> states = %{ "AL" => "Alabama", "WI" => "Wisconsin" }
%{"AL" => "Alabama", "WI" => "Wisconsin"}
iex> states["AL"]
"Alabama"
iex> states["TX"]
nil
```

# Difference Between Keyword Lists and Maps

Maps allow only one entry for a particular key, whereas keyword lists allow the key to be repeated.

How to Choose Between Maps and Keyword Lists:
* If you want to pattern-match against the contents.
  Map.
* If you want more than one entry with the same key.
  Keyword.
* If you want the elements to be ordered.
  Keyword.
* If none of the above.
  Map.

* Binaries: Ignore for now.

# Join Operators

`list1 ++ list2 # concatenates two lists`

`list1 -- list2 # returns elements in list1 not in list2`

# In Operator

`a in enum # tests if a is included in enum (for example, a list or a range)`

# Anonymous Functions

```elixir
fn
  parameter-list -> body
  parameter-list -> body ...
end
```

Can take multiple arguments, in order.

```elixir
iex> sum = fn (a, b) -> a + b end
#Function<12.17052888 in :erl_eval.expr/5>
iex> sum.(1, 2)
3
```

# Passing Functions

(`map` takes a function as an argument)

```elixir
iex> list = [1, 3, 5, 7, 9]
[1, 3, 5, 7, 9]
iex> Enum.map list, fn elem -> elem * 2 end
[2, 6, 10, 14, 18]
iex> Enum.map list, fn elem -> elem * elem end
[1, 9, 25, 49, 81]
iex> Enum.map list, fn elem -> elem > 6 end
[false, false, false, true, true]
```

# & Notation

```elixir
iex> add_one = &(&1 + 1) # same as add_one = fn (n) -> n + 1 end
#Function<6.17052888 in :erl_eval.expr/5>
iex> add_one.(44)
45
```

# Functions within a Module

```elixir
def greet(greeting, name), do: (
  IO.puts greeting
  IO.puts "How're you doing, #{name}?"
)
```

…and as a one-liner, with the Module definition

```elixir
defmodule Times do
  def double(n), do: n * 2
end
```

# Clauses

Elixir matches against the parameter to determine which one to use

```elixir
defmodule Factorial do
  def of(0), do: 1
  def of(n), do: n * of(n-1)
end
```

# Guard clauses

`when`

(in this example, negative numbers as parameters will produce a useful error)

```elixir
defmodule Factorial do
  def of(0), do: 1
  def of(n) when n > 0 do
n * of(n-1)
  end
end
```

# Default parameters

`\\`

```elixir
defmodule Example do
  def func(p1, p2 \\ 2, p3 \\ 3, p4) do
    IO.inspect [p1, p2, p3, p4]
  end
end
```

# Private Functions

Just use `defp`, very common for recursion clauses.

# Pipe Operator

(`|>`)

Do I even have to review this? It’s so cool.

Modules provide namespaces/wrappers

# Module attributes

prefix the key with `@`

`@name value`
