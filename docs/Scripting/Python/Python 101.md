---
authors: Emil Andrzejewski
date: 19.03.2025
weight: 0
---

# Python 101 :snake:

### Dictionaries
```py title="Iterating over dictionaries" linenums="1"
dict1 = {"a": 1, "b": 2, "c": 3}

for key, value in dict1.items():
  if value == 3:
    print(key)
```

```py title="Functions taking dictionaries as input" linenums="1"
def function7(**dict):
  for key, value in dict.items():
    print(key, value)

def function8(**ks):
  for a in ks:
    print(a, ks[a])

function7(a="1", b="2", c="3")
# Output: a 1 b 2 c 3

function8(a="1", b="2", c="3")
# Output: a 1 b 2 c 3
```
### Comprehensions
```py title="Basics" linenums="1"
list1 = ['a', 'b', 'c', 'd', 'e']
list2 = [x for x in list1]
print(list2)
# Output: ['a', 'b', 'c', 'd', 'e']

list3 = [c for c in "string"]
print(list3)
# Output: ['s', 't', 'r', 'i', 'n', 'g']

print("-".join(list11))
# Output: s-t-r-i-n-g
```

### Files
```py title="Basic file operations" linenums="1"
# Iterate over lines
with open("test.txt", encoding='latin-1') as f:
  for line in f:
    print(line)

# Append to a file
f = open("test.txt", "a")
f.write("test line two!")
f.close()
```

### Lambdas
```py title="Potentially useful lambdas" linenums="1"
blocks = lambda x, y: [x[i:i + y] for i in range(0, len(x), y)]
print(blocks("string", 2))
# Output: ["st", "ri", "ng"]

to_ord = lambda x: [ord(i) for i in x]
print(to_ord("ABCD"))
# Output: [65, 66, 67, 68]
```

```py title="Arithmetic operations examples" linenums="1"
add_4 = lambda x: x + 4
print(add_4(2))
# Output: 6

add = lambda x, y: x + y
print(add(2, 3))
# Output: 5

print((lambda x, y: x + y)(10, 4))
# Output 14

is_even = lambda x: x % 2 == 0
print(is_even(2))
# Output: True

print(is_even(3))
# Output: False
```