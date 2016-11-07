**Pattern matching**
```
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
```
iex>[1, \_, \_] = [1, 2, 3]
[1, 2, 3]
iex>[1, \_, \_] = [1, "cat", "dog"]
[1, "cat", "dog"]
```

**Pin operator (^)**
```
iex>a = 1
1
iex>a = 2
2
iex>^a = 1
**(MatchError) no match of right hand side value: 1
```

List — [ head | tail  ]
iex> list1 = [ 3, 2, 1  ]

[3, 2, 1]

iex> list2 = [ 4 | list1  ]

[4, 3, 2, 1]

Module.function(parameter)
ex. `String.capitalize name`

Types (with examples)
     Value
          Arbitrary-sized integers: decimal (1234), hexadecimal (0xcafe), octal (0o765), and binary (0b1010) — also with underscores (1_000_000)
          Floating-point numbers: 1.0, 0.2456, 0.314159e1, and 314159.0e-5
          Atoms: :fred, :is_binary?, :var@2, :<>, :===, :"func/3”, and :"long john silver"
Ranges: start..end (1..5, 123..156)
Regular expressions: Look it up, but remember to use the Regex module

     System
          PIDs and ports: PID is reference to a local or remote process and port is reference to a resource that you’ll be reading or writing.
          References: Ignore for now.

     Collection
          Tuples: Ordered collection of values, usually only 2 to 4 per tuple ({ 1, 2  }, { :ok, 42, "next”  }, { :error, :enoent  })
          Lists: a linked data structure, cheap to get the head and extract the tail (but not to access in random order), see above for example
               Keyword Lists: Elixir converts key/value pairs in a list into tuples ([ name: "Dave", city: "Dallas", likes: "Programming”  ] becomes [ {:name, "Dave"}, {:city, "Dallas"}, {:likes, "Programming"}  ])
          Maps: a collection of key/value pairs (%{ key => value, key => value  }, %{ { :error, :enoent  } => :fatal, { :error, :busy  } => :retry  })
               Accessing a map: Like a Ruby hash. Also, if the keys are atoms (:key), you can use dot notation (var.key).
iex> states = %{ "AL" => "Alabama", "WI" => "Wisconsin" }

%{"AL" => "Alabama", "WI" => "Wisconsin"}

iex> states["AL"]

"Alabama"

iex> states["TX"]

nil

          DIFFERENCE BETWEEN KEYWORD LIST AND MAP: Maps allow only one entry for a particular key, whereas keyword lists allow the key to be repeated.
          Binaries: Ignore for now.

Join Operators
list1 ++ list2 # concatenates two lists

list1 -- list2 # returns elements in list1 not in list2

“In" Operator
a in enum # tests if a is included in enum (for example,

# a list or a range)

Anonymous Function
parameter-list -> body ...



fn



parameter-list -> body



end

Can take multiple arguments, in order.

iex> sum = fn (a, b) -> a + b end

#Function<12.17052888 in :erl_eval.expr/5>

iex> sum.(1, 2)

3

Passing Functions (`map` takes a function as an argument)
iex> list = [1, 3, 5, 7, 9]

[1, 3, 5, 7, 9]

iex> Enum.map list, fn elem -> elem * 2 end

[2, 6, 10, 14, 18]

iex> Enum.map list, fn elem -> elem * elem end

[1, 9, 25, 49, 81]

iex> Enum.map list, fn elem -> elem > 6 end

[false, false, false, true, true]

& Notation
iex> add_one = &(&1 + 1) # same as add_one = fn (n) -> n + 1 end

#Function<6.17052888 in :erl_eval.expr/5>

iex> add_one.(44)

45

Functions within a Module

def greet(greeting, name), do: (

IO.puts greeting

IO.puts "How're you doing, #{name}?"


    )

…and as a one-liner, with the Module definition
defmodule Times do

def double(n), do: n * 2

end

Clauses — Elixir matches against the parameter to determine which one to use

defmodule Factorial do

 def of(0), do: 1

 def of(n), do: n * of(n-1)

end

Guard clauses — `when`
(in this example, negative numbers as parameters will produce a useful error)

 def of(0), do: 1

 def of(n) when n > 0 do

 n * of(n-1)

 end

end

defmodule Factorial do

Default parameters — `\\`

 def func(p1, p2 \\ 2, p3 \\ 3, p4) do

 IO.inspect [p1, p2, p3, p4]

 end

end

defmodule Example do

Private Functions
Just use `defp`, very common for recursion clauses.

Pipe Operator (|>)
Do I even have to review this? It’s so cool.

Modules provide namespaces/wrappers

Module attributes — prefix the key with `@`
@name value



`"
" }"
