---
authors: Emil Andrzejewski
date: 19.03.2025
weight: 1
---
### Requests
Introduction to requests module.

### Sys
[Official documentation](https://docs.python.org/3/library/sys.html "sys — System-specific parameters and functions")

```py title="Get info"
import sys
print(sys.version)
print(sys.executable) # Currently used Python binary
print(sys.platform)   # Currently used platform
print(sys.path)       # Packages path
print(sys.modules)    # Available modules
```

```py title="Process input from standard input"
for line in sys.stdin:
    if line.strip() == "exit":
        break
    sys.stdout.write(f">> {line}")
```

```py title="Print directly from standard output - in one line"
for i in range(1,5):
    sys.stdout.write(str(i))
    sys.stdout.flush()
    # Output: 1234
```

```py title="Loading bar using stdout"
import time

for i in range(0, 51):
    time.sleep(0.1)
    sys.stdout.write(f"{i} [{'#'*i}{'.'*(50-i)}]\r")
    sys.stdout.flush()
sys.stdout.write("\n")
```

```py title="Control user provided arguments"
print(sys.argv)
# Output: ['main.py']           - if ran without any arguments
# Output: ['main.py', '1', '2'] - if ran like "python main.py 1 2" (1)

if len(sys.argv) != 3:
    print(f"[X] To run {sys.argv[0]} enter a username and password!")
    sys.exit(5) # (2)

username = sys.argv[1]
password = sys.argv[2]

print(f"{username} {password}")

sys.exit(0) # (3)
```

1. **sys.argv** arguments are automatically casted as strings in an array.
2. Exit a script with a code of 5.
3. Exit a script with a code of 0.

!!! note "Exit code verification"
    To verify the exit code with which the program terminated, you can use the `echo $?` command in Bash.