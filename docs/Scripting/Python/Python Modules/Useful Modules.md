---
authors: Emil Andrzejewski
date: 19.03.2025
weight: 1
---
### sys
[Official documentation](https://docs.python.org/3/library/sys.html "sys — System-specific parameters and functions")

```py title="Get info" linenums="1"
import sys
print(sys.version)
print(sys.executable) # Currently used Python binary
print(sys.platform)   # Currently used platform
print(sys.path)       # Packages path
print(sys.modules)    # Available modules
```

```py title="Process input from standard input" linenums="1"
for line in sys.stdin:
    if line.strip() == "exit":
        break
    sys.stdout.write(f">> {line}")
```

```py title="Print directly from standard output - in one line" linenums="1"
for i in range(1,5):
    sys.stdout.write(str(i))
    sys.stdout.flush()
    # Output: 1234
```

```py title="Loading bar using stdout" linenums="1"
import time

for i in range(0, 51):
    time.sleep(0.1)
    sys.stdout.write(f"{i} [{'#'*i}{'.'*(50-i)}]\r")
    sys.stdout.flush()
sys.stdout.write("\n")
```

```py title="Control user provided arguments" linenums="1"
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

---

### requests
[Official documentation](https://requests.readthedocs.io/en/latest/ "Requests: HTTP for Humans")

```py title="Response data" linenums="1"
import requests

x = requests.get('http://httpbin.org/get')

print(x.status_code)
print(x.headers) # Response headers
print(x.cookies) # Cookies returned by the server in response
print(x.text)    # Response text
print(x.json())  # Response as json
print(x.elapsed) # Time elapsed between request being sent and getting a response
```

```py title="Sending different jazz" linenums="1"
# Defining request arguments
params = {'id': 3}
headers = {'Accept': 'application/json', 'test_header': 'test'}
cookies = {'a': 'b'}

x = requests.get('http://httpbin.org/get', params=params, headers=headers, cookies=cookies)
```

```py title="POST requests" linenums="1"
# Sending POST body data
x = requests.post('http://httpbin.org/post', data={'a':'b', 'c': 'd', 'e': 'f'})

# Sending file
files = {'file': open('test.txt', 'rb')}
x = requests.post('http://httpbin.org/post', files=files)
```

```py title="Misc operations" linenums="1"
# Basic Auth
x = requests.get('http://httpbin.org/get', auth=('username', 'password'))

# Bypass invalid SSL cert
x = requests.get('http://expired.badssl.com', verify=False)

# Disallow redirects
x = requests.get('http://github.com', allow_redirects=False)

# Set a response timeout
x = requests.get('http://httpbin.org/get', timeout=5)
print(x.content)

# Save file to disk
x = requests.get('https://www.google.com/images/branding/googlelogo/1x/googlelogo_light_color_272x92dp.png')
with open('google.png', 'wb') as f:
    f.write(x.content)
```

```py title="Sessions" linenums="1"
x = requests.Session()
x.cookies.update({'a': 'b'})
response = x.get('http://httpbin.org/cookies')
print(response.text)
```

---

### pwntools
[Official documentation](https://docs.pwntools.com/en/latest/# "pwntools")

```py title="Pwntools examples" linenums="1"
from pwn import *

print(cyclic(50))
print(cyclic_find("laaa"))

print(shellcraft.sh())
print(hexdump(asm(shellcraft.sh())))

# Run process
p = process("/bin/sh")
p.sendline("echo hello;")
p.interactive()

# Connect remotely
r = remote("127.0.0.1", 1234)
r.sendline("hello!")
r.interactive
r.close

# Packing numbers
print(p32(0x13371337))
print(hex(u32(p32(0x13371337))))

# Loading files
l = ELF('/bin/bash')

print(hex(l.address))
print(hex(l.entry))

print(hex(l.got['write']))
print(hex(l.plt['write']))

for address in l.search(b'/bin/sh\x00'):
    print(hex(address))

print(hex(next(l.search(asm('jmp esp')))))

r = ROP(l)
print(r.rbx)

# Different operations
print(xor(xor("A", "B"), "A"))
print(b64e("test"))
print(b64d("dGVzdA=="))
print(md5sumhex(b"hello"))
print(sha1sumhex(b"hello"))

print(bits(b'a'))
print(unbits([0,1,1,0,0,0,0,1]))
```

---