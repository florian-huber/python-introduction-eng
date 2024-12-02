# Clean Code and Best Practices

In the initial chapters, we covered several foundational concepts in Python:

- Various **data types**: Numbers, strings, lists, tuples, dictionaries, sets, booleans, and `None`
- `for` and `while` loops
- Conditionals: `if-elif-else`
- Logical expressions
- Functions
- Error handling with `try-except`
- Libraries

Now, let's take a step back to look at the **big picture**.

---

## Teams vs. the Lonely Hacker

We discussed teamwork and pair programming in more detail—these notes are currently only available in the slides on Moodle.

The session then transitioned into **code quality** and **clean code**, starting with:

---

### The Zen of Python

Try running this import in Python:

```python
import this
```

It should output the following:

```bash
The Zen of Python, by Tim Peters

Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```

Opinions differ on how sacred or ironic these Zen rules are and what exactly they mean. However, many of the rules revolve around writing code that is clear and readable.

------

## Clean Code and Best Practices

### Readability: Meaningful Names and Comments

Readable code is crucial, especially when working in teams. Using meaningful variable and function names and providing comments or docstrings is essential for understanding what the code is supposed to do.

For example, consider the following code:

```python
def handle_x(x):
    b = 9 / 5
    c = 32
    d = 273.15
    e = x - d
    return e * b + c

print(handle_x(400))
```

What does this function do? Now compare it to:

```python
def kelvin_to_fahrenheit(temp_kelvin: float):
    """Convert temperature from Kelvin to Fahrenheit."""
    fahrenheit_factor = 9 / 5
    fahrenheit_offset = 32
    absolute_zero = 273.15
    temp_celsius = temp_kelvin - absolute_zero
    return temp_celsius * fahrenheit_factor + fahrenheit_offset

print(kelvin_to_fahrenheit(400))
```

Here, the purpose of the function is immediately clear, as are the roles of the variables.

------

## Example: Rock-Paper-Scissors

Let’s program a game of Rock-Paper-Scissors where a human player competes against the computer. We'll start with a function for the computer to randomly choose one of the three options.

```python
import random

def rock_paper_scissor():
    """Returns randomly chosen string: 'rock', 'paper', or 'scissors'."""
    random_number = random.randint(1, 3)
    if random_number == 1:
        return "rock"
    if random_number == 2:
        return "paper"
    return "scissors"
```

Alternatively, we can simplify this using `random.choice()`:

```python
import random

def rock_paper_scissor():
    """Returns randomly chosen string: 'rock', 'paper', or 'scissors'."""
    return random.choice(["rock", "paper", "scissors"])
```

------

## Structuring the Game Logic

Here’s a simple implementation for the entire game:

```python
def play_game():
    print("Yes! Rock-Paper-Scissors!")
    computer_choice = rock_paper_scissor()
    print("What is your choice?")
    human_choice = input("a) rock, b) paper, c) scissors: ").lower()
    
    assert human_choice in ["a", "b", "c"], "Invalid input."
    
    options = {"a": "rock", "b": "paper", "c": "scissors"}
    human_choice = options[human_choice]
    
    print(f"Human: {human_choice} vs. Computer: {computer_choice}.")
    
    if human_choice == computer_choice:
        print("Draw!")
    elif (human_choice == "rock" and computer_choice == "scissors") or \
         (human_choice == "paper" and computer_choice == "rock") or \
         (human_choice == "scissors" and computer_choice == "paper"):
        print("Human wins!")
    else:
        print("Computer wins!")

play_game()
```

By breaking the logic into smaller functions, the game becomes more modular and easier to extend or debug. For example, you could add functions like `who_won` to handle the win logic separately or allow two human players to compete.

------

## Python Ecosystem

Python’s extensive ecosystem of libraries and tools is one of the key reasons for its success. So far, we’ve only worked with standard libraries like `time` and `random`.

However, many libraries must be installed before use. For example:

```
>>> import seaborn

ModuleNotFoundError: No module named 'seaborn'
```

Libraries can be installed using package managers such as `pip` or `conda`:

```
pip install seaborn
```

or:

```
conda install seaborn
```

### Managing Dependencies with Environments

Python libraries often depend on other libraries, which can lead to version conflicts. To avoid such conflicts, developers use **environments** to isolate dependencies for different projects. We will use **conda** to manage environments later in the course.

```
