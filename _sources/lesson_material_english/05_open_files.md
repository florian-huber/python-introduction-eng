# Reading and Writing Files

Files can generally be categorized into binary files and text files. Binary files consist of bit patterns and allow efficient data storage, often used in well-known formats like images, videos, or audio files. Such files usually require specialized tools or Python libraries for import. Text files, on the other hand, are readable with a standard text editor and include formats like `.txt`, `.csv`, `.yml`, or `.py`. These are the files we’ll primarily focus on.

---

## Reading Files

Files can be read in Python using the `open()` function. For example, consider a file named `testfile.txt` located in the same directory:

```python
data = open("testfile.txt", "r")
print(data.readline())  # => 'Here is some sample text for testing.\n'
```

Here, the `"r"` argument specifies the mode in which the file is opened. The following table summarizes the most common modes:

| **Mode** | **Meaning**                     | **Explanation**                                                                                     |
|----------|---------------------------------|-----------------------------------------------------------------------------------------------------|
| `r`      | Read mode, text                 | Cursor starts at the beginning of the file. Does not create new files.                             |
| `rb`     | Read mode, binary               |                                                                                                     |
| `w`      | Write mode, text                | Overwrites existing files or creates a new file.                                                   |
| `wb`     | Write mode, binary              |                                                                                                     |
| `a`      | Append mode, text               | Writes to the end of the file without overwriting the existing content.                            |
| `ab`     | Append mode, binary             |                                                                                                     |
| `x`      | Exclusive creation, text        | Fails if the file exists.                                                                           |
| `xb`     | Exclusive creation, binary      |                                                                                                     |

---

### Reading Line by Line

You can also read a file line by line:

```python
data = open("testfile.txt", "r")
for line in data:
    print(line)
```

If the file isn’t in the same folder, you need to provide the file path. 

- **Windows:** Use `"C:/User/my_folder/testfile.txt"` or escape backslashes like `"C:\\User\\my_folder\\testfile.txt"`.
- **macOS/Linux:** Use `"/home/user/my_folder/testfile.txt"`.

You can also use *relative paths*:
```python
data = open("my_data/testfile2.txt", "r")
```

For advanced path handling, consider using libraries like `os`.

---

## Writing Files

To write to a file, use the `write()` method. First, open a file in write mode:

```python
output = open("output_file.txt", "w")
text = "Now for something completely different."
output.write(text + "\n")
output.close()
```

With mode `"w"`, a new file is created each time. To append to an existing file instead, use `"a"`:

```python
output = open("output_file.txt", "a")
output.write("Yes. Exactly.\n")
output.write("Yes " * 5 + "\n")
output.close()
```

---

### Using `with` for File Management

A common and recommended approach is to use the `with` statement for file handling. This ensures the file is properly closed, even if an error occurs.

```python
with open("output_file.txt", "w") as file:
    for i in range(1, 6):
        file.write(f"Line {i} \n")
```

Reading a file with `with`:

```python
with open("output_file.txt", "r") as file:
    for line in file:
        if "3" in line:
            print(line)
```

---

## Encoding

Computers don't inherently understand letters or characters—only bytes, which are numbers from 0 to 255. To map these numbers to characters, encoding systems are used.

### ASCII

ASCII (*American Standard Code for Information Interchange*) can represent 256 characters. However, it lacks many special characters.

### Unicode

Unicode has become the standard, especially for the web (HTML 4.0), supporting over 100,000 characters. The most commonly used Unicode encoding in Python is **UTF-8**, as it efficiently represents characters while saving space.

For more on encoding, refer to the [SelfHTML Wiki on character encoding](https://wiki.selfhtml.org/wiki/Zeichencodierung).

---

### Handling Encoding in Python

If you encounter issues with special characters (e.g., umlauts), it’s often due to improper conversion between ASCII and UTF-8. To avoid such problems, explicitly specify the encoding:

```python
with open("output_file.txt", "w", encoding="utf-8") as file:
    for i in range(1, 6):
        file.write(f"Line {i} \n")
```