# Python Assignment - Full Question-wise Study Sheet

## Q1. What is the difference between @property, getter, and setter in Python? Write a class Temperature that stores temperature in Celsius. Use @property to create a getter that returns the temperature in Fahrenheit, and a setter that validates the input — raise a ValueError if temperature is below -273.15°C (absolute zero).

**Topic to read on W3Schools:** Python Class Properties, Python Classes/Objects, Python Encapsulation

A getter reads a value. A setter changes a value. `@property` makes a method act like a normal attribute. It is useful when you want to protect data but still keep the class easy to use. Here, the class stores Celsius internally and shows Fahrenheit when the property is read.

**Program:**

```python
class Temperature:
    def __init__(self, celsius):
        # store the real temperature internally
        self._celsius = 0
        self.celsius = celsius

    @property
    def celsius(self):
        # return temperature in Fahrenheit
        return (self._celsius * 9 / 5) + 32

    @celsius.setter
    def celsius(self, value):
        # do not allow values below absolute zero
        if value < -273.15:
            raise ValueError("Temperature cannot be below -273.15°C")

        self._celsius = value


# create object
t = Temperature(25)

# getter is called here
print(t.celsius)

# setter is called here
t.celsius = 30
print(t.celsius)
```

## Q2. Explain generators in Python. What is the difference between a normal function and a generator function? Write a generator function squares(n) that yields squares of numbers from 1 to n. Also show how next() and a for loop work with it.

**Topic to read on W3Schools:** Python Generators, Python Iterators, Python Functions

A normal function runs fully and returns one result. A generator function pauses at `yield` and gives values one by one. This is useful when you want to save memory and produce values slowly instead of all at once.

**Program:**

```python
def squares(n):
    # start from 1
    i = 1

    while i <= n:
        # give one square value at a time
        yield i * i
        i = i + 1


# create generator object
g = squares(5)

# get values one by one
print(next(g))
print(next(g))

# loop through a fresh generator
for value in squares(5):
    print(value)
```

## Q3. Write a Python program using OOP to implement a Stack data structure with push(), pop(), peek(), is_empty(), and display(). Use operator overloading to compare two stacks using ==. Demonstrate with at least two stack objects.

**Topic to read on W3Schools:** Python OOP, Python Classes/Objects, Python Polymorphism, Python Encapsulation

A stack works like a pile of plates. The last item added is the first item removed. `push()` adds an item, `pop()` removes the top item, `peek()` shows the top item, `is_empty()` checks whether the stack is empty, and `display()` prints all items. `==` is overloaded so two stacks can be compared by their content.

**Program:**

```python
class Stack:
    def __init__(self):
        # empty list used to store stack items
        self.items = []

    def push(self, value):
        # add item to top
        self.items.append(value)

    def pop(self):
        # stop if stack has no item
        if len(self.items) == 0:
            raise IndexError("Stack is empty")

        return self.items.pop()

    def peek(self):
        # show last item without removing it
        if len(self.items) == 0:
            return None

        return self.items[len(self.items) - 1]

    def is_empty(self):
        # return True if stack has no item
        return len(self.items) == 0

    def display(self):
        # print stack from bottom to top
        i = 0
        while i < len(self.items):
            print(self.items[i], end=" ")
            i = i + 1
        print()

    def __eq__(self, other):
        # compare two stacks item by item
        return self.items == other.items


# create two stack objects
s1 = Stack()
s2 = Stack()

# push values into both stacks
s1.push(10)
s1.push(20)
s2.push(10)
s2.push(20)

print("Equal:", s1 == s2)
print("Peek s1:", s1.peek())
print("Peek s2:", s2.peek())

s1.display()
s2.display()
```

## Q4. Define function. What is the difference between system defined and user defined function in python?

**Topic to read on W3Schools:** Python Functions

A function is a reusable block of code that does one task. System-defined functions are already built into Python, such as `print()` or `len()`. User-defined functions are written by the programmer using `def`.

## Q5. What is the difference between @staticmethod and @classmethod in Python? Illustrate with an example.

**Topic to read on W3Schools:** Python Class Methods, Python Functions, Python Classes/Objects

`@staticmethod` is a method inside a class, but it does not automatically receive `self` or `cls`. `@classmethod` receives the class itself as its first parameter, so it can work with class-level data.

**Program:**

```python
class Demo:
    count = 0

    @staticmethod
    def add(a, b):
        # simple helper method
        return a + b

    @classmethod
    def show_count(cls):
        # class method can read class variable
        return cls.count


print(Demo.add(2, 3))
print(Demo.show_count())
```

## Q6. Write a module to check prime number.

**Topic to read on W3Schools:** Python Modules, Python Functions

A prime number is a number that has only two divisors: 1 and itself. The program below checks that rule in a simple way.

**Program:**

```python
def is_prime(n):
    # numbers less than 2 are not prime
    if n <= 1:
        return False

    # 2 is prime
    if n == 2:
        return True

    # even numbers greater than 2 are not prime
    if n % 2 == 0:
        return False

    # check only odd numbers
    i = 3
    while i * i <= n:
        if n % i == 0:
            return False
        i = i + 2

    return True


num = 29

if is_prime(num):
    print("Prime")
else:
    print("Not Prime")
```

## Q7. What will be the output of the following program? Justify your answer.
a = [1, 2, 3]
b = a
c = a[:]
a.append(4)
print(b)
print(c)

**Topic to read on W3Schools:** Python Lists, Python Variables

b and a point to the same list, so when a changes, b also changes. c is a copy made using slicing, so it keeps the old values.

**Program:**

```python
a = [1, 2, 3]
b = a      # same list reference
c = a[:]   # separate copy

a.append(4)  # change original list

print(b)
print(c)
```

Output:
```python
[1, 2, 3, 4]
[1, 2, 3]
```

## Q8. Explain packages with the help of an example.

**Topic to read on W3Schools:** Python Modules, Python File Handling

A package is a folder that contains modules. It is used to keep a big project organized by splitting code into smaller files.

**Program:**

```python
# file: math_utils.py

def add(a, b):
    # return the sum
    return a + b

def multiply(a, b):
    # return the product
    return a * b


# file: main.py

from math_utils import add, multiply

print(add(2, 3))
print(multiply(4, 5))
```

## Q9. Explain the concept of __init__, __str__, and __repr__ in Python OOP. When would you use __repr__ over __str__?

**Topic to read on W3Schools:** Python __init__ Method, Python Classes/Objects, Python OOP

`__init__` is the constructor that runs when the object is created. `__str__` gives a clean readable form for users. `__repr__` gives a more exact form that is useful for debugging.

**Program:**

```python
class Student:
    def __init__(self, name, roll_no, marks):
        # store values at object creation
        self.name = name
        self.roll_no = roll_no
        self.marks = marks

    def __str__(self):
        # readable output for users
        return self.name + " " + str(self.roll_no) + " " + str(self.marks)

    def __repr__(self):
        # exact output for debugging
        return "Student(name='" + self.name + "', roll_no=" + str(self.roll_no) + ", marks=" + str(self.marks) + ")"


s = Student("Aarif", 12, 89)

print(s)
print(repr(s))
```

## Q10. Write a Python code that interchanges the first and last characters of a given string.

**Topic to read on W3Schools:** Python Strings, Python String Slicing

Strings are immutable, so we cannot change them directly. We create a new string with the first and last characters swapped.

**Program:**

```python
def swap_first_last(text):
    # keep short strings unchanged
    if len(text) < 2:
        return text

    first = text[0]
    last = text[len(text) - 1]
    middle = text[1:len(text) - 1]

    # build a new string
    return last + middle + first


s = "hello"
print(swap_first_last(s))
```

## Q11. Write a Python program using NumPy to create a 4×4 identity matrix, replace its diagonal elements with 5, and compute its determinant.

**Topic to read on W3Schools:** Python NumPy Tutorial

An identity matrix has 1 on the diagonal and 0 everywhere else. Replacing the diagonal with 5 changes the matrix, and the determinant tells us its overall effect.

**Program:**

```python
import numpy as np

# create identity matrix
m = np.eye(4)

# replace diagonal one by one
i = 0
while i < 4:
    m[i][i] = 5
    i = i + 1

print(m)

# compute determinant
print(np.linalg.det(m))
```

## Q12. Explain exception handling in Python with an example.

**Topic to read on W3Schools:** Python Try...Except, Python Exceptions

Exception handling means catching an error before the program crashes. `try` contains risky code, `except` handles the error, `else` runs only when no error happens, and `finally` runs no matter what.

**Program:**

```python
try:
    # risky code
    a = 10
    b = 0
    c = a / b
    print(c)

except ZeroDivisionError:
    # handle divide by zero
    print("Cannot divide by zero")

else:
    # runs only when no error happens
    print("No error")

finally:
    # runs always
    print("Program finished")
```

## Q13. Write a Python program using Pandas to read a CSV file marks.csv, find the average marks of each student, and display the top 5 students in descending order of their average.

**Topic to read on W3Schools:** Python Pandas Tutorial, Python File Handling

Read the CSV file, group the rows by student, calculate the average marks, sort the result from highest to lowest, and print the top five.

**Program:**

```python
import pandas as pd

# read csv file into a DataFrame
df = pd.read_csv("marks.csv")

# find average marks for each student
result = df.groupby("student")["marks"].mean().reset_index()

# sort by average marks in descending order
result = result.sort_values(by="marks", ascending=False)

# print top 5 students
print(result.head(5))
```

## Q14. Explain basic functionality of match() function?

**Topic to read on W3Schools:** Python RegEx

`match()` checks whether a pattern is found at the start of a string. If it matches, we get a match object. If not, we get `None`.

**Program:**

```python
import re

# input string
text = "abc123"

# pattern to match at the beginning
pattern = r"abc"

m = re.match(pattern, text)

if m:
    print("Matched")
else:
    print("Not matched")
```

## Q15. Explain the difference between loc and iloc in Pandas with examples. What error is raised when an invalid label is used with loc?

**Topic to read on W3Schools:** Python Pandas Tutorial

`loc` uses labels like row names or column names. `iloc` uses integer positions. If a wrong label is given to `loc`, Pandas raises `KeyError`.

**Program:**

```python
import pandas as pd

data = {
    "name": ["A", "B", "C"],
    "marks": [80, 90, 70]
}

df = pd.DataFrame(data)

# label-based access
print(df.loc[0])

# position-based access
print(df.iloc[0])
```

## Q16. Write about map and filter in Python?

**Topic to read on W3Schools:** Python Lambda, Python Functions

`map()` applies a function to every item in a sequence. `filter()` keeps only the items that satisfy a condition. Both are useful for short and neat data processing.

**Program:**

```python
numbers = [1, 2, 3, 4, 5]

# square every number
squares = list(map(lambda x: x * x, numbers))
print(squares)

# keep only even numbers
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))
print(even_numbers)
```

## Q17. What will be the output of the following program? Explain how Python resolves method calls using MRO.
class A:
    def greet(self): print("Hello from A")
class B(A):
    def greet(self): print("Hello from B")
class C(A):
    def greet(self): print("Hello from C")
class D(B, C): pass
d = D()
d.greet()
print(D.__mro__)

**Topic to read on W3Schools:** Python Inheritance, Python Polymorphism

MRO means Method Resolution Order. It tells Python which class to search first when a method is called. In `D(B, C)`, Python checks B first, then C, then A.

**Program:**

```python
class A:
    def greet(self):
        print("Hello from A")

class B(A):
    def greet(self):
        print("Hello from B")

class C(A):
    def greet(self):
        print("Hello from C")

class D(B, C):
    pass

# create object of D
d = D()

# Python uses MRO to find greet()
d.greet()

# print method resolution order
print(D.__mro__)
```

Output:
```python
Hello from B
(<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>)
```

## Q18. What will be the output of following program? Assume that user will enter only integer value.

temp = input("Enter a number: ")
x = temp * 0
y = int(temp) * 0
z = bool(temp * 0)

print(x)
print(y)
print(z)

**Topic to read on W3Schools:** Python User Input, Python Strings, Python Casting, Python Booleans

`input()` gives a string. A string multiplied by 0 becomes an empty string. `int(temp) * 0` becomes `0`. `bool()` becomes `False`.

**Program:**

```python
temp = input("Enter a number: ")

# string multiplied by 0 becomes empty string
x = temp * 0

# integer multiplied by 0 becomes 0
y = int(temp) * 0

# empty string is False in boolean form
z = bool(temp * 0)

print(x)
print(y)
print(z)
```

Output for any integer input:
```python

0
False
```

## Q19. Examine how python supports regular expressions through 're' module with an example?

**Topic to read on W3Schools:** Python RegEx

The `re` module is used for searching and matching patterns in text. It is useful when the text follows a fixed structure.

**Program:**

```python
import re

# text to search
text = "My number is 98765"

# regular expression for digits
pattern = r"\d+"

m = re.search(pattern, text)

if m:
    print(m.group())
```

## Q20. Define a class BankAccount with attributes account_number, holder_name, and balance. Implement methods to deposit(), withdraw(), and display() the account details. Use encapsulation to protect the balance from direct access. Demonstrate with at least one object.

**Topic to read on W3Schools:** Python Classes/Objects, Python Encapsulation, Python OOP

Encapsulation means keeping important data safe inside the class. `deposit()` adds money, `withdraw()` removes money only if enough balance exists, and `display()` shows the account details.

**Program:**

```python
class BankAccount:
    def __init__(self, account_number, holder_name, balance):
        # store details
        self.account_number = account_number
        self.holder_name = holder_name
        self._balance = balance

    def deposit(self, amount):
        # add money only if amount is positive
        if amount > 0:
            self._balance = self._balance + amount

    def withdraw(self, amount):
        # remove money only if balance is enough
        if amount > 0 and amount <= self._balance:
            self._balance = self._balance - amount
        else:
            print("Not enough balance")

    def display(self):
        # print all account details
        print("Account No:", self.account_number)
        print("Holder Name:", self.holder_name)
        print("Balance:", self._balance)


acc = BankAccount(101, "Aarif", 5000)
acc.deposit(1000)
acc.withdraw(2000)
acc.display()
```

## Q21. What is Multithreading in Python and How to achieve it?

**Topic to read on W3Schools:** Python Modules, Python File Handling

Multithreading means running more than one task at the same time. Python uses the `threading` module for this, especially for I/O work like waiting on files or web requests.

**Program:**

```python
import threading

def worker():
    # work done by the thread
    print("Thread is running")

# create thread object
t = threading.Thread(target=worker)

# start the thread
t.start()

# wait for thread to finish
t.join()
```

## Q22. Explain the use of __init__() constructor with an example. Write a class Student that uses a constructor to initialize name, roll_no, and marks. Also define a __str__() method to display the student details in a readable format.

**Topic to read on W3Schools:** Python __init__ Method, Python Classes/Objects

`__init__` runs when the object is created. It is used to give starting values to the object.

**Program:**

```python
class Student:
    def __init__(self, name, roll_no, marks):
        # constructor sets initial values
        self.name = name
        self.roll_no = roll_no
        self.marks = marks

    def __str__(self):
        # readable form
        return self.name + " " + str(self.roll_no) + " " + str(self.marks)


s = Student("Aarif", 12, 89)
print(s)
```

## Q23. Determine the output of the program and justify your answer with step-by-step evaluation based on operator precedence and associativity rules.

a = 10
b = 5
c = 2
d = 3

result = a + b * c ** d // b - d
result += (a > b) and (c < d) or (b == c)
result += (a & b | c ^ d)
result += (~c + (a << 2) - (b >> 1))
result += (a in [10, 20, 30])
result += (b is c)

print("Final Result =", result)

**Topic to read on W3Schools:** Python Operators, Python Booleans, Python Lists

This question uses operator precedence, bitwise operators, comparison operators, membership, and identity checks. The final value must be found step by step.

**Program:**

```python
a = 10
b = 5
c = 2
d = 3

result = a + b * c ** d // b - d
result += (a > b) and (c < d) or (b == c)
result += (a & b | c ^ d)
result += (~c + (a << 2) - (b >> 1))
result += (a in [10, 20, 30])
result += (b is c)

print("Final Result =", result)
```

Final answer:
```python
Final Result = 53
```

## Q24. What are *args and **kwargs in Python? Write a function student_info(name, *subjects, **details) that accepts a student's name, any number of subjects, and additional keyword details like age and grade. Display all the received values inside the function.

**Topic to read on W3Schools:** Python Arguments, Python Functions

`*args` collects extra positional values into a tuple. `**kwargs` collects extra named values into a dictionary. This makes the function flexible.

**Program:**

```python
def student_info(name, *subjects, **details):
    # print fixed value
    print("Name:", name)

    # print subjects one by one
    print("Subjects:")
    i = 0
    while i < len(subjects):
        print(subjects[i])
        i = i + 1

    # print extra key-value details
    print("Details:")
    for key in details:
        print(key, details[key])


student_info("Aarif", "Math", "Physics", age=20, grade="A")
```

## Q25. What is a decorator in Python? Write a decorator function check_positive that checks whether the argument passed to a function is a positive number. If not, it should print an error message instead of calling the function. Demonstrate it on a function square_root(n).

**Topic to read on W3Schools:** Python Decorators, Python Functions

A decorator is a wrapper around a function. It adds extra work before the real function runs. Here it checks whether the number is positive first.

**Program:**

```python
def check_positive(func):
    def wrapper(n):
        # stop negative or zero input
        if n <= 0:
            print("Error: number must be positive")
        else:
            return func(n)
    return wrapper


@check_positive
def square_root(n):
    # simple square root calculation
    print(n ** 0.5)


square_root(16)
square_root(-4)
```

## Q26. Develop a Python program to manage student records using both text and binary files with exception handling.

**Topic to read on W3Schools:** Python File Handling, Python Try...Except, Python Modules

This program stores student records in a binary file, keeps a text log file, searches and updates records, and uses exception handling so the program does not crash. A custom exception is used for marks outside 0 to 100.

**Program:**

```python
import pickle
from datetime import datetime

class InvalidMarksError(Exception):
    # custom error when marks are invalid
    pass

DATA_FILE = "students.dat"
LOG_FILE = "log.txt"

def log_message(message):
    # write message with time
    f = open(LOG_FILE, "a")
    f.write(str(datetime.now()) + " - " + message + "\n")
    f.close()

def validate_marks(marks):
    # marks should be between 0 and 100
    if marks < 0 or marks > 100:
        raise InvalidMarksError("Marks must be between 0 and 100")

def load_records():
    try:
        f = open(DATA_FILE, "rb")
    except FileNotFoundError:
        # file does not exist yet
        return []

    try:
        records = pickle.load(f)
        f.close()
        return records
    except EOFError:
        # empty file
        f.close()
        return []

def save_records(records):
    # overwrite file with updated list
    f = open(DATA_FILE, "wb")
    pickle.dump(records, f)
    f.close()

def add_students():
    records = load_records()

    count = int(input("How many students? "))
    i = 0
    while i < count:
        try:
            roll = int(input("Roll number: "))
            name = input("Name: ")
            marks = float(input("Marks: "))

            validate_marks(marks)

            record = {"roll": roll, "name": name, "marks": marks}
            records.append(record)

            print("Added successfully")
            log_message("Added student roll " + str(roll))

        except InvalidMarksError as e:
            print(e)
            log_message("Error: " + str(e))
        except ValueError:
            print("Invalid input")
            log_message("Error: invalid user input")
        except Exception as e:
            print("Runtime error:", e)
            log_message("Error: " + str(e))

        i = i + 1

    save_records(records)

def display_all():
    try:
        records = load_records()

        if len(records) == 0:
            print("No records found")
            return

        i = 0
        while i < len(records):
            print(records[i])
            i = i + 1

        log_message("Displayed all records")

    except Exception as e:
        print("Error:", e)
        log_message("Error: " + str(e))

def search_student():
    try:
        records = load_records()
        roll = int(input("Enter roll number to search: "))

        found = False
        i = 0
        while i < len(records):
            if records[i]["roll"] == roll:
                print("Record found:", records[i])
                found = True
                break
            i = i + 1

        if found:
            log_message("Searched student roll " + str(roll))
        else:
            print("Student not found")
            log_message("Search failed for roll " + str(roll))

    except ValueError:
        print("Invalid input")
        log_message("Error: invalid user input")
    except Exception as e:
        print("Error:", e)
        log_message("Error: " + str(e))

def update_marks():
    try:
        records = load_records()
        roll = int(input("Enter roll number to update: "))
        new_marks = float(input("Enter new marks: "))

        validate_marks(new_marks)

        found = False
        i = 0
        while i < len(records):
            if records[i]["roll"] == roll:
                records[i]["marks"] = new_marks
                found = True
                break
            i = i + 1

        if found:
            save_records(records)
            print("Marks updated")
            log_message("Updated marks for roll " + str(roll))
        else:
            print("Student not found")
            log_message("Update failed for roll " + str(roll))

    except InvalidMarksError as e:
        print(e)
        log_message("Error: " + str(e))
    except ValueError:
        print("Invalid input")
        log_message("Error: invalid user input")
    except Exception as e:
        print("Error:", e)
        log_message("Error: " + str(e))

def menu():
    while True:
        print("\n1. Add students")
        print("2. Display all")
        print("3. Search student")
        print("4. Update marks")
        print("5. Exit")

        choice = input("Enter choice: ")

        if choice == "1":
            add_students()
        elif choice == "2":
            display_all()
        elif choice == "3":
            search_student()
        elif choice == "4":
            update_marks()
        elif choice == "5":
            break
        else:
            print("Invalid choice")

menu()
```

## Q27. A company wants to develop a program to manage details of its employees using the concept of inheritance in Python. Create a base class named Employee that contains Employee ID, Name, Basic Salary. Derive Manager with Allowance and Bonus. Derive Developer with Overtime hours and Overtime rate. Display total salary for both.

**Topic to read on W3Schools:** Python Inheritance, Python Polymorphism, Python Classes/Objects

Inheritance means one class gets the features of another class. Here Employee is the base class, and Manager and Developer are child classes that add their own salary rules.

**Program:**

```python
class Employee:
    def __init__(self, emp_id=0, name="", basic_salary=0):
        self.emp_id = emp_id
        self.name = name
        self.basic_salary = basic_salary

    def accept(self):
        # common employee details
        self.emp_id = int(input("Employee ID: "))
        self.name = input("Name: ")
        self.basic_salary = float(input("Basic Salary: "))

    def display(self):
        # print base details
        print("Employee ID:", self.emp_id)
        print("Name:", self.name)
        print("Basic Salary:", self.basic_salary)

class Manager(Employee):
    def __init__(self):
        Employee.__init__(self)
        self.allowance = 0
        self.bonus = 0

    def accept(self):
        Employee.accept(self)
        # extra manager fields
        self.allowance = float(input("Allowance: "))
        self.bonus = float(input("Bonus: "))

    def total_salary(self):
        return self.basic_salary + self.allowance + self.bonus

    def display(self):
        Employee.display(self)
        print("Allowance:", self.allowance)
        print("Bonus:", self.bonus)
        print("Total Salary:", self.total_salary())

class Developer(Employee):
    def __init__(self):
        Employee.__init__(self)
        self.overtime_hours = 0
        self.overtime_rate = 0

    def accept(self):
        Employee.accept(self)
        # extra developer fields
        self.overtime_hours = float(input("Overtime Hours: "))
        self.overtime_rate = float(input("Overtime Rate: "))

    def total_salary(self):
        return self.basic_salary + (self.overtime_hours * self.overtime_rate)

    def display(self):
        Employee.display(self)
        print("Overtime Hours:", self.overtime_hours)
        print("Overtime Rate:", self.overtime_rate)
        print("Total Salary:", self.total_salary())

m = Manager()
d = Developer()

print("Enter Manager details")
m.accept()

print("\nEnter Developer details")
d.accept()

print("\nManager Details")
m.display()

print("\nDeveloper Details")
d.display()
```

## Q28. Explain lambda functions in Python. Write a Python program that uses a lambda function along with map() to square all elements of a list, and filter() to keep only even numbers from another list.

**Topic to read on W3Schools:** Python Lambda, Python Functions

A lambda is a small one-line function without a name. It is useful for short tasks like squaring a number or checking whether a number is even.

**Program:**

```python
numbers1 = [1, 2, 3, 4]
numbers2 = [5, 6, 7, 8, 9]

# square all values in first list
squares = list(map(lambda x: x * x, numbers1))

# keep only even values in second list
evens = list(filter(lambda x: x % 2 == 0, numbers2))

print(squares)
print(evens)
```

## Q29. What is the difference between mutable and immutable data types in Python? Explain with examples of list, tuple, string, and dictionary. What happens when you try to modify an immutable object?

**Topic to read on W3Schools:** Python Lists, Python Tuples, Python Strings, Python Dictionaries

Mutable means the value can change after creation. Immutable means it cannot change after creation. Lists and dictionaries are mutable. Tuples and strings are immutable. If you try to change an immutable object, Python raises an error.

**Program:**

```python
my_list = [1, 2, 3]
my_tuple = (1, 2, 3)
my_string = "abc"
my_dict = {"a": 1}

# mutable objects can be changed
my_list[0] = 10
my_dict["a"] = 20

print(my_list)
print(my_dict)

# these lines would cause errors
# my_tuple[0] = 10
# my_string[0] = 'z'
```

## Q30. Explain the four pillars of Object Oriented Programming with a real-life example for each. Which pillar is demonstrated by method overriding and why?

**Topic to read on W3Schools:** Python OOP, Python Inheritance, Python Polymorphism, Python Encapsulation

The four pillars are Encapsulation, Inheritance, Polymorphism, and Abstraction. Encapsulation hides data, Inheritance gives child classes the features of parent classes, Polymorphism lets one method name work in different ways, and Abstraction shows only the important details. Method overriding demonstrates polymorphism because the child class changes the behavior of the same method name.

## Q31. What is the difference between append(), extend(), and insert() in a Python list? Write a program that demonstrates all three methods and also shows how to remove an element using remove() and pop().

**Topic to read on W3Schools:** Python Lists, Python Lists Methods

`append()` adds one item at the end. `extend()` adds many items at the end. `insert()` adds one item at a chosen position. `remove()` deletes by value, and `pop()` deletes and returns an item by index.

**Program:**

```python
items = [1, 2, 3]

# add values
items.append(4)
items.extend([5, 6])
items.insert(1, 10)

print(items)

# remove by value
items.remove(10)
print(items)

# remove and store last item
last_item = items.pop()
print(last_item)
print(items)
```

## Q32. What is the difference between raise, try, except, else, and finally in Python exception handling? Write a program that demonstrates all five keywords together with a user-defined exception NegativeAgeError.

**Topic to read on W3Schools:** Python Try...Except, Python Exceptions

`raise` creates an error. `try` contains risky code. `except` handles the error. `else` runs only when no error happens. `finally` runs always. A user-defined exception is a custom error class made by the programmer.

**Program:**

```python
class NegativeAgeError(Exception):
    # custom exception for invalid age
    pass

try:
    # read age from user
    age = int(input("Enter age: "))

    # raise our own error if age is negative
    if age < 0:
        raise NegativeAgeError("Age cannot be negative")

except NegativeAgeError as e:
    print(e)

except ValueError:
    print("Invalid input")

else:
    print("Age accepted")

finally:
    print("End of program")
```

## Q33. Design a Python class hierarchy for a Bank Account System with abstract Account, SavingsAccount, CurrentAccount, custom exception InsufficientFundsError, __str__, and polymorphism.

**Topic to read on W3Schools:** Python OOP, Python Inheritance, Python Polymorphism, Python Encapsulation

This question mixes abstract classes, custom exceptions, inheritance, and polymorphism. The base class stores common account details. The child classes handle their own interest logic. A single list can hold different account types and call the same method on all of them.

**Program:**

```python
from abc import ABC, abstractmethod

class InsufficientFundsError(Exception):
    # custom exception when money is not enough
    pass

class Account(ABC):
    def __init__(self, holder_name, balance):
        self.holder_name = holder_name
        self.balance = balance

    def deposit(self, amount):
        # add money to account
        self.balance = self.balance + amount

    def withdraw(self, amount):
        # stop if balance is too low
        if amount > self.balance:
            raise InsufficientFundsError("Not enough balance")

        self.balance = self.balance - amount

    def __str__(self):
        # readable account information
        return "Holder: " + self.holder_name + ", Balance: " + str(self.balance)

    @abstractmethod
    def calculate_interest(self):
        pass

class SavingsAccount(Account):
    def calculate_interest(self):
        # 4% interest
        return self.balance * 0.04

class CurrentAccount(Account):
    def calculate_interest(self):
        # no interest for current account
        return 0

accounts = [
    SavingsAccount("A", 10000),
    CurrentAccount("B", 5000)
]

i = 0
while i < len(accounts):
    print(accounts[i])
    print(accounts[i].calculate_interest())
    i = i + 1
```

## Q34. Concurrency — AsyncIO vs Threading (Marks: 15). Write asyncio code, compare threading/multiprocessing/asyncio, write thread-safe counter and broken version, and explain GIL.

**Topic to read on W3Schools:** Python Modules, Python Try...Except, Python File Handling

Threading is good for waiting tasks, multiprocessing is better for CPU-heavy tasks, and AsyncIO is good for many network calls. The GIL is a lock in CPython that allows only one thread to run Python bytecode at a time.

**Program:**

```python
import asyncio
import aiohttp
import threading

URLS = [
    "https://www.google.com",
    "https://www.python.org",
    "https://www.github.com",
    "https://www.wikipedia.org",
    "https://www.stackoverflow.com"
]

async def fetch_status(session, url):
    try:
        # set 5-second timeout for each request
        timeout = aiohttp.ClientTimeout(total=5)

        async with session.get(url, timeout=timeout) as response:
            return url, response.status

    except asyncio.TimeoutError:
        return url, "TimeoutError"

    except aiohttp.ClientError:
        return url, "ConnectionError"

    except Exception:
        return url, "Error"

async def main():
    async with aiohttp.ClientSession() as session:
        tasks = []

        # build task list one by one
        i = 0
        while i < len(URLS):
            tasks.append(fetch_status(session, URLS[i]))
            i = i + 1

        # run all requests together
        results = await asyncio.gather(*tasks)

        # print results
        i = 0
        while i < len(results):
            print(results[i][0], "->", results[i][1])
            i = i + 1

# thread-safe counter example
safe_count = 0
unsafe_count = 0
lock = threading.Lock()

def safe_worker():
    global safe_count
    i = 0
    while i < 1000:
        lock.acquire()
        safe_count = safe_count + 1
        lock.release()
        i = i + 1

def unsafe_worker():
    global unsafe_count
    i = 0
    while i < 1000:
        unsafe_count = unsafe_count + 1
        i = i + 1

# run asyncio part
asyncio.run(main())
```

## Q35. Generators and Iterators. Write read_errors(filename), parse_errors(lines), and Fibonacci using both a generator and an iterator class.

**Topic to read on W3Schools:** Python Generators, Python Iterators, Python File Handling

A generator gives one value at a time and saves memory. An iterator is an object that can be used in a loop and returns one item at a time.

**Program:**

```python
def read_errors(filename):
    # open file and yield only error lines
    f = open(filename, "r")
    for line in f:
        if "ERROR" in line:
            yield line.strip()
    f.close()

def parse_errors(lines):
    # convert each line into a dictionary
    for line in lines:
        parts = line.split(" ", 3)

        if len(parts) == 4:
            record = {
                "timestamp": parts[0] + " " + parts[1],
                "level": parts[2],
                "message": parts[3]
            }
            yield record

def fibonacci_generator(n):
    # generator version of Fibonacci
    a = 0
    b = 1
    i = 0

    while i < n:
        yield a
        temp = a + b
        a = b
        b = temp
        i = i + 1

class FibonacciIterator:
    # iterator version of Fibonacci
    def __init__(self, n):
        self.n = n
        self.i = 0
        self.a = 0
        self.b = 1

    def __iter__(self):
        return self

    def __next__(self):
        if self.i >= self.n:
            raise StopIteration

        value = self.a
        temp = self.a + self.b
        self.a = self.b
        self.b = temp
        self.i = self.i + 1
        return value

# chain both generators
parsed = parse_errors(read_errors("server.log"))

count = 0
for item in parsed:
    print(item)
    count = count + 1
    if count == 3:
        break

print("Generator Fibonacci:")
for x in fibonacci_generator(5):
    print(x)

print("Iterator Fibonacci:")
for x in FibonacciIterator(5):
    print(x)
```
## Notes

Some advanced topics in your assignment do not have a single exact W3Schools page name, especially AsyncIO, aiohttp, and some file-serialization details. For those, the closest W3Schools reading topics are:
Python Modules, Python File Handling, Python OOP, Python Inheritance, Python Polymorphism, Python Try...Except, Python Generators, Python Iterators, Python RegEx, Python Functions, Python Lambda, Python Class Methods, and Python Class Properties.

Source assignment: fileciteturn2file0