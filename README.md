# README.md

## 🔐 Automating Allow List Maintenance with Python

This project showcases a simple yet powerful Python script designed to help cybersecurity professionals manage and sanitize allow lists of IP addresses. With automation becoming increasingly important in secure environments, this lab demonstrates how to safely update a file-based IP allow list by removing any entries found in a separate block or removal list.

---

## 📁 About the Project

In real-world security environments, teams often manage lists of approved IP addresses that are allowed to access sensitive content. Over time, certain IPs must be revoked due to changes in policy, threat detection, or decommissioned devices.

This script automatically:

- Reads a file (`allow_list.txt`) containing allowed IP addresses
- Compares it against a Python list of IPs to remove (`remove_list`)
- Filters out any disallowed IPs
- Overwrites the original file with the updated list

The entire process is efficient, secure, and Pythonic.

---

## 🧠 Key Features

- **Safe File Handling** using Python's `with` context manager
- **Efficient Filtering** with a list comprehension
- **Clean File Rewrite** using `.join()` and `.write()` methods
- **Human-Readable Code** suitable for junior and senior engineers alike

---

## 🚀 Example Code

```python
def update_file(import_file, remove_list):
    with open(import_file, "r") as file:
        ip_addresses = file.read()

    ip_addresses = ip_addresses.split()
    ip_addresses = [ip for ip in ip_addresses if ip not in remove_list]
    ip_addresses = "\n".join(ip_addresses)

    with open(import_file, "w") as file:
        file.write(ip_addresses)
```

---

## ✅ Why This Matters

This lab highlights:

- Good Python practices (no list mutation during iteration)
- Real-world relevance for cybersecurity workflows
- Thoughtful commenting and step-by-step breakdown (see `FULL_LAB.md`)

---

## 📎 How to Use

1. Create or supply a text file named `allow_list.txt` containing space- or line-separated IP addresses.
2. Define a Python list of IPs to remove:
   ```python
   remove_list = ["192.168.0.1", "10.0.0.1"]
   ```
3. Call the function:
   ```python
   update_file("allow_list.txt", remove_list)
   ```
4. The file will be automatically cleaned and updated.

---

## 👨‍💻 Author Notes

This project was completed as part of my cybersecurity portfolio to demonstrate my ability to write clean, maintainable Python code for real-world security operations tasks.

See the `FULL_LAB.md` file for an educational walkthrough.

---

## 📜 License

MIT License

