# 💣 Ransomware Bruteforce Recovery Lab
<p align="center">
  <img src="https://img.shields.io/badge/python-3.9%2B-blue.svg" alt="Python 3.9+">
  <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="MIT License">
  <img src="https://img.shields.io/badge/project-status-Completed-brightgreen.svg" alt="Project Status">
  <img src="https://img.shields.io/badge/type-Cybersecurity%20Lab-purple.svg" alt="Cybersecurity Lab">
  <img src="https://img.shields.io/badge/task-Forage%20SOC%20Challenge-orange.svg" alt="Forage SOC Challenge">
</p>

**Challenge:** AIG Cybersecurity Program – Task 2  
**Objective:** Recover a ransomware-encrypted ZIP file by bruteforcing the password using Python and a RockYou-derived wordlist.

---

## 🧠 Scenario

A zero-day vulnerability (Log4Shell) was exploited in the Product Development Staging Environment, allowing an attacker to install a ransomware payload. Fortunately, only one ZIP file was encrypted before the attack was stopped. Rather than pay the ransom, I wrote a Python script to recover the file by bruteforcing the encryption key.

---

## 🔧 Tools Used

- Python 3.9+
- `zipfile` module (standard library)
- `rockyou.txt` (common password wordlist subset)

---

## 🧪 Methodology

1. Loaded a list of passwords from `rockyou.txt`
2. Iterated through each password, attempting to extract the contents of `enc.zip`
3. On success, printed the password and terminated
4. On failure, continued trying other passwords

---

## 🐍 bruteforce.py

```python
from zipfile import ZipFile

def attempt_extract(zf_handle, password):
    try:
        zf_handle.extractall(pwd=password)
        print(f"[+] Password found: {password.decode()}")
        return True
    except:
        return False

def main():
    print("[+] Beginning bruteforce ")
    with ZipFile('enc.zip') as zf:
        with open('rockyou.txt', 'rb') as f:
            for line in f:
                password = line.strip()
                if attempt_extract(zf, password):
                    return
    print("[-] Password not found in list")

if __name__ == "__main__":
    main()
```

## 🔐 Output
```markdown
[+] Beginning bruteforce
[+] Password found: SPONGEBOB
```


---

## 📄 Decrypted File

The `.docx` file inside `enc.zip` was successfully extracted using the cracked password. The final document included instructions to paste this code as part of the submission.

---

## 🧠 Lessons Learned

- Ransomware often relies on weak or reused payloads that can be reversed with common tools.
- Brute-forcing can be a practical recovery method in isolated cases when mitigation is urgent and legal.
- Always log passwords tried and structure your code for readability and reusability during an IR event.

---

## 📁 Folder Structure

Shields Up - Cybersecurity/

├── enc.zip 

├── rockyou.txt 

├── bruteforce.py 

└── README.md

---

## 🔖 Tags

`#python` `#ransomware` `#infosec` `#bruteforce` `#zipfile` `#SOCChallenge` `#ForageAIG`
