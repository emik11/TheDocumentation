## Files
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
## Lambdas
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