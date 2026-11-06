# CLI CAMS – Questions and Answers - 6th November 2026.

### 1. Khushi Rani: What command checks the contents of a directory?

**Answer:** Use `ls` to list files and folders. Use `ls -la` to include hidden files and details.

### 2. Anoop Vantagodi: What is the use of `.get()` in a Python dictionary?

**Answer:** `.get()` retrieves a value using its key. If the key is missing, it returns `None` or a default value instead of raising a `KeyError`.

```python
marks = {"Math": 90}
print(marks.get("Science", 0))  # 0
```

### 3. Kummari Amaresh: How do you clone a Git repository?

**Answer:** Run `git clone <repository-url>` to copy a remote repository onto your computer.

### 4. Kuppireddy Sivashankara Reddy: What is the difference between `.` and `..`?

**Answer:** `.` means the current directory. `..` means the parent directory.

### 5. Manish Nalumachu: What is the difference between `git checkout` and `git switch`?

**Answer:** `git switch` is mainly used to change branches. `git checkout` can change branches and restore files or check out specific commits.

### 6. Masarpu Jyothish: What command shows an IP address?

**Answer:** Run `ip addr` to see IP addresses on Linux.

### 7. Mohd Saad Shaikh: Why is unit testing useful?

**Answer:** Unit testing checks small parts of code individually, helping find bugs early and making changes safer.

### 8. Moyya Naveen: Why do we use `sort` before `uniq`?

**Answer:** `uniq` removes only adjacent duplicate lines. `sort` brings matching lines together.

```bash
sort names.txt | uniq
```

### 9. Mudrakola Sai Pavan: What is the difference between a set and a dictionary?

**Answer:** A **set** stores unique values. A **dictionary** stores key-value pairs.

```python
numbers = {1, 2, 3}
student = {"name": "Ravi", "age": 21}
```

### 10. Neha Sunil Magadum: What are comments in Python?

**Answer:** Comments are notes in code for humans to read. Python ignores `#` comments when running the program.

```python
# This is a comment
```

### 11. Palepu Veerababu: What is the use of `pstree`?

**Answer:** `pstree` displays running processes in a tree, showing parent and child processes.

### 12. Parameswaran R: What is the use of `wget`?

**Answer:** `wget` downloads files from the internet using the command line.

```bash
wget https://example.com/file.zip
```

### 13. Pavan Kumar: Does Python support constructor overloading?

**Answer:** No, Python does not support traditional constructor overloading using multiple `__init__` methods. You can use default arguments or `*args` instead.

### 14. Raghu B S: How can we reset the last Git commit?

**Answer:** Use `git reset --soft HEAD~1` to undo the last local commit while keeping its changes staged.

### 15. Shakthivel: What is the difference between shallow copy and deep copy?

**Answer:** A shallow copy copies the outer object but shares nested objects. A deep copy creates separate copies of nested objects too.

### 16. Sunkara Prasanth: How can we edit a tuple?

**Answer:** Tuples are immutable, so you cannot directly change their elements. Create a new tuple instead.

### 17. Varad Rajesh Barbhai: What is an SSH key?

**Answer:** An SSH key pair has a private key and a public key. It allows secure authentication to servers or Git services without entering a password each time. Keep the private key secret.
