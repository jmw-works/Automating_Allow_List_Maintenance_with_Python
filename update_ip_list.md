# Update a file through a Python algorithm

## Project description

At my organization, access to restricted content is controlled with an allow list of IP addresses. The `allow_list.txt` file identifies these IP addresses. A separate remove list identifies IP addresses that should no longer have access to this content. I created an algorithm to automate updating the `allow_list.txt` file and remove these IP addresses that should no longer have access.

---

## Open the file that contains the allow list

For the first part of the algorithm, I opened the `allow_list.txt` file. First, I assigned this file name as a string to the `import_file` variable:

```python
import_file = "allow_list.txt"
```

Then, I used a `with` statement to open the file:

```python
with open(import_file, "r") as file:
    ip_addresses = file.read()
```

In my algorithm, the `with` statement is used with the `.open()` function in read mode to open the allow list file for the purpose of reading it. The purpose of opening the file is to allow me to access the IP addresses stored in the allow list file. The `with` keyword helps manage resources by closing the file after exiting the statement. In the code `with open(import_file, "r") as file:`, the `open()` function has two parameters. The first identifies the file to import, and the second indicates what I want to do with the file. In this case, "r" indicates that I want to read it. The code also uses the `as` keyword to assign a variable named `file`; `file` stores the output of the `.open()` function while I work within the `with` statement.

---

## Read the file contents

In order to read the file contents, I used the `.read()` method to convert it into a string:

```python
ip_addresses = file.read()
```

When using an `.open()` function that includes the argument "r" for “read,” I can call the `.read()` function in the body of the `with` statement. The `.read()` method converts the file into a string and allows me to read it. I applied the `.read()` method to the `file` variable identified in the `with` statement. Then, I assigned the string output of this method to the variable `ip_addresses`.

In summary, this code reads the contents of the `allow_list.txt` file into a string format that allows me to later use the string to organize and extract data in my Python program.

---

## Convert the string into a list

In order to remove individual IP addresses from the allow list, I needed it to be in list format. Therefore, I used the `.split()` method to convert the `ip_addresses` string into a list:

```python
ip_addresses = ip_addresses.split()
```

The `.split()` function is called by appending it to a string variable. It works by converting the contents of a string to a list. The purpose of splitting `ip_addresses` into a list is to make it easier to remove IP addresses from the allow list. By default, the `.split()` function splits the text by whitespace into list elements. In this algorithm, the `.split()` function takes the data stored in the variable `ip_addresses`, which is a string of IP addresses that are each separated by a whitespace, and it converts this string into a list of IP addresses. To store this list, I reassigned it back to the variable `ip_addresses`.

---

## Remove IP addresses that are on the remove list

My algorithm requires removing any IP address from the allow list, `ip_addresses`, that is also contained in `remove_list`. To do this more safely and efficiently than using `.remove()` in a loop, I used a list comprehension:

```python
ip_addresses = [ip for ip in ip_addresses if ip not in remove_list]
```

This list comprehension builds a new list by including only those IP addresses from `ip_addresses` that are **not** found in `remove_list`. It avoids modifying the list while iterating over it, which could otherwise result in errors or skipped elements. Here's a breakdown:

- `ip for ip in ip_addresses`: loop through each IP in the original list
- `if ip not in remove_list`: include only IPs that are **not** in `remove_list`
- The entire expression inside brackets `[...]` builds a new, filtered list

This is a cleaner, more reliable alternative to using a `for` loop with `.remove()`.

---

## Update the file with the revised list of IP addresses

As a final step in my algorithm, I needed to update the allow list file with the revised list of IP addresses. To do so, I first needed to convert the list back into a string. I used the `.join()` method for this:

```python
ip_addresses = "\n".join(ip_addresses)
```

The `.join()` method combines all items in an iterable into a string. The `.join()` method is applied to a string containing characters that will separate the elements in the iterable once joined into a string. In this algorithm, I used the `.join()` method to create a string from the list `ip_addresses` so that I could pass it in as an argument to the `.write()` method when writing to the file `allow_list.txt`. I used the string (`"\n"`) as the separator to instruct Python to place each element on a new line.

Then, I used another `with` statement and the `.write()` method to update the file:

```python
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

This time, I used a second argument of "w" with the `open()` function in my `with` statement. This argument indicates that I want to open a file to write over its contents. When using this argument "w", I can call the `.write()` function in the body of the `with` statement. The `.write()` function writes string data to a specified file and replaces any existing file content.

In this case I wanted to write the updated allow list as a string to the file `allow_list.txt`. This way, the restricted content will no longer be accessible to any IP addresses that were removed from the allow list. To rewrite the file, I appended the `.write()` function to the file object `file` that I identified in the `with` statement. I passed in the `ip_addresses` variable as the argument to specify that the contents of the file should be replaced with the data in this variable.

---

## Summary

I created an algorithm that removes IP addresses identified in a `remove_list` variable from the `allow_list.txt` file of approved IP addresses. This algorithm involved opening the file, converting it to a string to be read, and then converting this string to a list stored in the variable `ip_addresses`. Rather than using a `for` loop with `.remove()`, I applied a list comprehension to efficiently and safely filter out any IP addresses found in `remove_list`. After this, I used the `.join()` method to convert the updated list of IP addresses back into a string, placing each on a new line. Finally, I used the `.write()` method to overwrite the contents of the `allow_list.txt` file with this revised list, ensuring that access is revoked for any IPs listed in the remove list.

