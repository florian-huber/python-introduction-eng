# Getting Started with Python

In this course, we will learn programming using the Python programming language. Python will also accompany you throughout the rest of your DAISY studies, as we will use it in many lectures and projects. To get started with Python at home, you first need to install Python on your own computer. There are various ways to do this, and in many cases, Python is already pre-installed (e.g., on Macs).

If Python is not pre-installed, it can be downloaded from the official website: [python.org](https://www.python.org/). However, for this course, we need more than just the programming language itself, so we recommend a more comprehensive solution:

## Installing Python

### Python and Anaconda

The simplest and most convenient way to work with Python is by installing **Anaconda**, a software package that is free for students. Anaconda includes Python along with many useful libraries and tools specifically designed for Data Science and Artificial Intelligence. One such tool is the integrated development environment (IDE) **Spyder**, which makes writing and running Python code easier.

You can download Anaconda here: [Anaconda download link](https://www.anaconda.com/download/success)

Select the "Free Download" version; no email registration is necessary (simply click "skip registration"). When installing on **Windows**, ensure you check the box asking whether to add Anaconda to your `PATH`. This is important so Python can be recognized in the command line.

### Alternative: Miniconda

For those who are already familiar with their computer or prefer a minimal installation, we recommend [**Miniconda**](https://docs.anaconda.com/miniconda/). Miniconda only installs the essential components, and you can later decide which additional libraries you need. However, this requires a bit more configuration.

### How to Run Python

Once Python (via Anaconda or Miniconda) is installed, there are various ways to execute Python code. The main methods we will use in this course are the command line and the integrated development environment (IDE) Spyder.

### Python in the Command Line

An easy way to run Python is through the **command line** (or terminal on Mac/Linux). To do this, open the command line and enter the command `python` or `python3`, depending on how Python is set up on your system. You should now see a Python prompt that looks something like this:

```
Python 3.x.x (default, ...)
[GCC ...] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

Here, you can enter simple Python commands and execute them immediately. For example:
```
>>> print("Hello, World!")
```

### Python in the IDE Spyder

A more user-friendly way to use Python is through the integrated development environment (IDE) **Spyder**, which comes with Anaconda but is also freely available as open-source software. Spyder provides a graphical user interface where you can write, execute, and view the results of your code. Here’s how you work with Spyder:

1. **Editor:** In Spyder's main window, you write your Python code in the editor. Here, you can create larger programs or scripts consisting of multiple lines of code.
2. **Run:** To execute your code, click the green "Play" button at the top of the window or press the `F5` key. The code will run, and the results will appear in the **console**.
3. **Variable Explorer:** Another advantage of Spyder is the **Variable Explorer**, which allows you to see all variables currently being used in your program. This is particularly useful for managing large datasets, which is often the case in Data Science.

Spyder is a powerful environment for writing and debugging Python code. It offers many features to help you work efficiently, such as code completion, syntax highlighting, and built-in debugging tools. Later in your studies, many of you may switch to other editors, especially **Visual Studio Code**, which offers even more features. However, for beginners, Spyder is often more straightforward, which is why we will use it in this semester's course.

Most of the program code we write will be created in the **editor**. This allows us to write extensive code across multiple lines and save it as `.py` files. Like most IDEs for Python, Spyder also regularly provides hints about potential errors or other helpful suggestions. It’s also important to note that we can create not only code but also comments.

## Comments in Python

When programming, it is often helpful to include comments in your code to explain specific sections or make notes for yourself or other developers. Comments are ignored by the Python interpreter and have no impact on the program's execution. There are two ways to add comments in Python:

**Single-line Comments**

Single-line comments use the hash symbol `#`. Everything following the `#` is treated as a comment and ignored. For example:
```python
# This is a comment
print("Hello, World!")  # This is another comment
```

In the example above, the line with the `print` command is executed, while the comment is ignored.

**Multi-line Comments**

For **multi-line comments**, Python does not have a specific syntax, but you can use triple quotes (`"""` or `'''`) to create a **docstring**. Although docstrings are primarily used for documenting functions or classes, they can also be used for longer comments in code:

```python
"""
This is a multi-line comment.
It can be used to add detailed explanations or documentation.
"""
print("Hello, World!")
```

## Running Python Code

Once Python is installed on your computer, there are several ways to execute your Python code. Depending on the use case, you can choose between the **command line**, an integrated development environment (IDE) like **Spyder**, or specialized editors like **Visual Studio Code**.

### Running Python Scripts from the Command Line

If you have written a Python script and want to run it outside an IDE, you can easily do so via the **command line** (or terminal on Mac/Linux). For example, suppose you have a script named `my_script.py` that you want to execute.

Here’s how:

1. **Navigate** to the directory where your script is saved using the terminal/command line.

   On Windows, use the `cd` (Change Directory) command to navigate to the appropriate folder:

   ```bash 
   cd Folder1/Folder2
   ```

   On Mac/Linux, the process is similar:

   ```bash
   cd /Folder1/Folder2
   ```

2. **Run your script** by entering the command `python` or `python3` (depending on your installation), followed by the name of your script:

   ```bash
   python my_script.py
   ```

   This will start the Python interpreter, which will execute your script line by line. For example, if your script contains a simple output like `print("Hello, World!")`, it will be displayed directly in the command line.

### Benefits of Running Scripts from the Command Line

- **Direct Control:** You have full control over how your script is started and can explicitly specify different Python versions if multiple are installed (e.g., `python3 my_script.py` for Python 3).
- **Simple Automation:** Scripts can easily be integrated with other tools or automated using batch files or shell scripts.
- **Lightweight:** No additional graphical interface is required, making it ideal for quick tests or running Python programs on servers.
