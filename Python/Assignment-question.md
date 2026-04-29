# Python Assignment - Full Question-wise Study Sheet

Source document: fileciteturn2file0

## Q1. What is the difference between @property, getter, and setter in Python? Write a class Temperature that stores temperature in Celsius. Use @property to create a getter that returns the temperature in Fahrenheit, and a setter that validates the input — raise a ValueError if temperature is below -273.15°C (absolute zero).

**Topic to read on W3Schools:** Python Class Properties, Python Classes/Objects, Python Encapsulation

A getter is used to read a value, a setter is used to change a value, and `@property` lets a method behave like a normal attribute. It makes the class easier to use and lets us protect the data. In this question, we keep the real temperature in Celsius, but show Fahrenheit when the property is read.

```python
class Temperature:
    def __init__(self, celsius):
        self._celsius = 0
        self.celsius = celsius

    @property
    def celsius(self):
        return (self._celsius * 9 / 5) + 32

    @celsius.setter
    def celsius(self, value):
        if value < -273.15:
            raise ValueError("Temperature cannot be below -273.15°C")
        self._celsius = value


t = Temperature(25)
print(t.celsius)
t.celsius = 30
print(t.celsius)
```

## Q2. Explain generators in Python. What is the difference between a normal function and a generator function? Write a generator function squares(n) that yields squares of numbers from 1 to n. Also show how next() and a for loop work with it.

**Topic to read on W3Schools:** Python Generators, Python Iterators, Python Functions

A normal function runs from start to end and gives one final result. A generator function pauses at `yield` and remembers where it stopped. This is useful when you want values one by one and do not want to store all of them in memory.

```python
def squares(n):
    i = 1
    while i <= n:
        yield i * i
        i = i + 1


g = squares(5)
print(next(g))
print(next(g))

for value in squares(5):
    print(value)
```

## Q3. Write a Python program using OOP to implement a Stack data structure with the following methods: push(), pop(), peek(), is_empty(), and display(). Use operator overloading to compare two stacks using ==. Demonstrate with at least two stack objects.

**Topic to read on W3Schools:** Python OOP, Python Classes/Objects, Python Polymorphism, Python Encapsulation

A stack works like a pile of plates: the last item added is the first item removed. `push()` adds an item, `pop()` removes the top item, `peek()` shows the top item, `is_empty()` checks whether anything is inside, and `display()` prints all items. `==` is overloaded so two stacks can be compared by contents.

```python
class Stack:
    def __init__(self):
        self.items = []

    def push(self, value):
        self.items.append(value)

    def pop(self):
        if len(self.items) == 0:
            raise IndexError("Stack is empty")
        return self.items.pop()

    def peek(self):
        if len(self.items) == 0:
            return None
        return self.items[len(self.items) - 1]

    def is_empty(self):
        return len(self.items) == 0

    def display(self):
        i = 0
        while i < len(self.items):
            print(self.items[i], end=" ")
            i = i + 1
        print()

    def __eq__(self, other):
        return self.items == other.items


s1 = Stack()
s2 = Stack()

s1.push(10)
s1.push(20)
s2.push(10)
s2.push(20)

print("Equal:", s1 == s2)
print("Top of s1:", s1.peek())
print("Top of s2:", s2.peek())

s1.display()
s2.display()
```

## Q4. Define function. What is the difference between system defined and user defined function in python?

**Topic to read on W3Schools:** Python Functions

A function is a reusable block of code that does one job. A system-defined function is already available in Python, like `print()` or `len()`. A user-defined function is the one you create yourself using `def`.

## Q5. What is the difference between @staticmethod and @classmethod in Python? Illustrate with an example.

**Topic to read on W3Schools:** Python Class Methods, Python Functions, Python Classes/Objects

`@staticmethod` is a method inside a class, but it does not automatically get `self` or `cls`. `@classmethod` gets the class itself as its first parameter, so it can work with class-level data.

```python
class Demo:
    count = 0

    @staticmethod
    def add(a, b):
        return a + b

    @classmethod
    def show_count(cls):
        return cls.count


print(Demo.add(2, 3))
print(Demo.show_count())
```

## Q6. Write a module to check prime number.

**Topic to read on W3Schools:** Python Modules, Python Functions

A prime number is a number that has only two divisors: 1 and itself. The module below checks whether a number is prime.

```python
def is_prime(n):
    if n <= 1:
        return False

    if n == 2:
        return True

    if n % 2 == 0:
        return False

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

`b = a` makes both names point to the same list. `c = a[:]` makes a copy. So when `a` changes, `b` changes too, but `c` stays the same.

```python
a = [1, 2, 3]
b = a
c = a[:]
a.append(4)
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

A package is just a folder that contains modules. It helps keep a big program organized. Instead of putting everything in one file, we split the code into smaller files.

Example structure:
```text
my_package/
    __init__.py
    math_utils.py
    string_utils.py
```

Example use:
```python
# math_utils.py
def add(a, b):
    return a + b

def multiply(a, b):
    return a * b
```

```python
# main.py
from math_utils import add, multiply

print(add(2, 3))
print(multiply(4, 5))
```

## Q9. Explain the concept of __init__, __str__, and __repr__ in Python OOP. When would you use __repr__ over __str__?

**Topic to read on W3Schools:** Python __init__ Method, Python Classes/Objects, Python OOP

`__init__` is the constructor, so it runs when an object is created. `__str__` is for a nice readable output. `__repr__` is for a more exact and developer-friendly output, mainly useful when debugging.

```python
class Student:
    def __init__(self, name, roll_no, marks):
        self.name = name
        self.roll_no = roll_no
        self.marks = marks

    def __str__(self):
        return self.name + " " + str(self.roll_no) + " " + str(self.marks)

    def __repr__(self):
        return "Student(name='" + self.name + "', roll_no=" + str(self.roll_no) + ", marks=" + str(self.marks) + ")"


s = Student("Aarif", 12, 89)
print(s)
print(repr(s))
```

## Q10. Write a Python code that interchanges the first and last characters of a given string.

**Topic to read on W3Schools:** Python Strings, Python String Slicing

Strings cannot be changed directly because they are immutable. So we make a new string with the first and last characters swapped.

```python
def swap_first_last(text):
    if len(text) < 2:
        return text

    first = text[0]
    last = text[len(text) - 1]
    middle = text[1:len(text) - 1]
    return last + middle + first


s = "hello"
print(swap_first_last(s))
```

## Q11. Write a Python program using NumPy to create a 4×4 identity matrix, replace its diagonal elements with 5, and compute its determinant.

**Topic to read on W3Schools:** Python NumPy Tutorial

An identity matrix has 1 on the diagonal and 0 everywhere else. After replacing the diagonal with 5, the determinant changes. The program below does it step by step.

```python
import numpy as np

m = np.eye(4)

i = 0
while i < 4:
    m[i][i] = 5
    i = i + 1

print(m)
print(np.linalg.det(m))
```

## Q12. Explain exception handling in Python with an example.

**Topic to read on W3Schools:** Python Try...Except, Python Exceptions

Exception handling means catching an error before the program stops. `try` contains the risky code, `except` catches the error, `else` runs only if no error happened, and `finally` runs no matter what.

```python
try:
    a = 10
    b = 0
    c = a / b
    print(c)
except ZeroDivisionError:
    print("Cannot divide by zero")
else:
    print("No error")
finally:
    print("Program finished")
```

## Q13. Write a Python program using Pandas to read a CSV file marks.csv, find the average marks of each student, and display the top 5 students in descending order of their average.

**Topic to read on W3Schools:** Python Pandas Tutorial, Python File Handling

Read the CSV, group the rows by student, calculate the average marks, sort the results, and show the top 5.

```python
import pandas as pd

df = pd.read_csv("marks.csv")

result = df.groupby("student")["marks"].mean().reset_index()
result = result.sort_values(by="marks", ascending=False)

print(result.head(5))
```

## Q14. Explain basic functionality of match() function?

**Topic to read on W3Schools:** Python RegEx

`match()` checks whether a pattern is found at the beginning of a string. If it matches, you get a match object. If not, you get `None`.

```python
import re

text = "abc123"
pattern = r"abc"

m = re.match(pattern, text)
if m:
    print("Matched")
else:
    print("Not matched")
```

## Q15. Explain the difference between loc and iloc in Pandas with examples. What error is raised when an invalid label is used with loc?

**Topic to read on W3Schools:** Python Pandas Tutorial

`loc` uses labels, while `iloc` uses integer positions. If a wrong label is used with `loc`, Pandas raises `KeyError`.

```python
import pandas as pd

data = {
    "name": ["A", "B", "C"],
    "marks": [80, 90, 70]
}
df = pd.DataFrame(data)

print(df.loc[0])
print(df.iloc[0])
```

## Q16. Write about map and filter in Python?

**Topic to read on W3Schools:** Python Lambda, Python Functions

`map()` applies a function to every item. `filter()` keeps only the items that satisfy a condition.

```python
numbers = [1, 2, 3, 4, 5]

squares = list(map(lambda x: x * x, numbers))
print(squares)

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

MRO means Method Resolution Order. It tells Python which class to check first when a method is called. In `D(B, C)`, Python checks `B` first, then `C`, then `A`, so `greet()` from `B` is used.

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

d = D()
d.greet()
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

`input()` gives a string. A string multiplied by 0 becomes an empty string. `int(temp) * 0` becomes `0`. `bool("")` becomes `False`.

```python
temp = input("Enter a number: ")
x = temp * 0
y = int(temp) * 0
z = bool(temp * 0)

print(x)
print(y)
print(z)
```

## Q19. Examine how python supports regular expressions through 're' module with an example?

**Topic to read on W3Schools:** Python RegEx

The `re` module is used for searching and matching patterns inside text. It is helpful when the text follows a fixed format.

```python
import re

text = "My number is 98765"
pattern = r"\d+"

m = re.search(pattern, text)
if m:
    print(m.group())
```

## Q20. Define a class BankAccount with attributes account_number, holder_name, and balance. Implement methods to deposit(), withdraw(), and display() the account details. Use encapsulation to protect the balance from direct access. Demonstrate with at least one object.

**Topic to read on W3Schools:** Python Classes/Objects, Python Encapsulation, Python OOP

Encapsulation means hiding the important data so it is not changed directly by mistake. The balance is treated like protected data here. `deposit()` adds money, `withdraw()` removes money only when enough balance is available, and `display()` prints the full details.

```python
class BankAccount:
    def __init__(self, account_number, holder_name, balance):
        self.account_number = account_number
        self.holder_name = holder_name
        self._balance = balance

    def deposit(self, amount):
        if amount > 0:
            self._balance = self._balance + amount

    def withdraw(self, amount):
        if amount > 0 and amount <= self._balance:
            self._balance = self._balance - amount
        else:
            print("Not enough balance")

    def display(self):
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

Multithreading means running more than one task at the same time. Python uses the `threading` module for this. It is useful for waiting-type tasks like network requests or file work.

```python
import threading

def worker():
    print("Thread is running")

t = threading.Thread(target=worker)
t.start()
t.join()
```

## Q22. Explain the use of __init__() constructor with an example. Write a class Student that uses a constructor to initialize name, roll_no, and marks. Also define a __str__() method to display the student details in a readable format.

**Topic to read on W3Schools:** Python __init__ Method, Python Classes/Objects

`__init__` is called when the object is created. It is used to set the starting values of the object.

```python
class Student:
    def __init__(self, name, roll_no, marks):
        self.name = name
        self.roll_no = roll_no
        self.marks = marks

    def __str__(self):
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

This question is about operator precedence, bitwise operators, comparison operators, membership, and identity checks. The final value is found step by step.

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

`*args` collects extra positional values. `**kwargs` collects extra named values. This makes the function flexible.

```python
def student_info(name, *subjects, **details):
    print("Name:", name)

    print("Subjects:")
    i = 0
    while i < len(subjects):
        print(subjects[i])
        i = i + 1

    print("Details:")
    for key in details:
        print(key, details[key])


student_info("Aarif", "Math", "Physics", age=20, grade="A")
```

## Q25. What is a decorator in Python? Write a decorator function check_positive that checks whether the argument passed to a function is a positive number. If not, it should print an error message instead of calling the function. Demonstrate it on a function square_root(n).

**Topic to read on W3Schools:** Python Decorators, Python Functions

A decorator is a wrapper around a function. It adds extra work before the original function runs. Here it checks the number first.

```python
def check_positive(func):
    def wrapper(n):
        if n <= 0:
            print("Error: number must be positive")
        else:
            return func(n)
    return wrapper


@check_positive
def square_root(n):
    result = n ** 0.5
    print(result)


square_root(16)
square_root(-4)
```

## Q26. Develop a Python program to manage student records using both text and binary files with exception handling.

**Topic to read on W3Schools:** Python File Handling, Python Try...Except, Python Modules

This program stores student records in a binary file using `pickle`, keeps a text log file, searches by roll number, updates marks, and uses a custom exception for invalid marks.

```python
import pickle
from datetime import datetime

class InvalidMarksError(Exception):
    pass

DATA_FILE = "students.dat"
LOG_FILE = "log.txt"

def log_message(message):
    f = open(LOG_FILE, "a")
    f.write(str(datetime.now()) + " - " + message + "\n")
    f.close()

def load_records():
    try:
        f = open(DATA_FILE, "rb")
    except FileNotFoundError:
        return []

    try:
        records = pickle.load(f)
        f.close()
        return records
    except EOFError:
        f.close()
        return []

def save_records(records):
    f = open(DATA_FILE, "wb")
    pickle.dump(records, f)
    f.close()

def validate_marks(marks):
    if marks < 0 or marks > 100:
        raise InvalidMarksError("Marks must be between 0 and 100")

def add_students():
    records = load_records()

    count = int(input("How many students do you want to add? "))
    i = 0
    while i < count:
        try:
            roll = int(input("Roll number: "))
            name = input("Name: ")
            marks = float(input("Marks: "))
            validate_marks(marks)

            record = {"roll": roll, "name": name, "marks": marks}
            records.append(record)
            log_message("Added student roll " + str(roll))
            print("Added successfully")

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

## Q27. A company wants to develop a program to manage details of its employees using the concept of inheritance in Python. Create a base class named Employee ... derive Manager and Developer ... display total salary.

**Topic to read on W3Schools:** Python Inheritance, Python Polymorphism, Python Classes/Objects

Inheritance means a child class gets the common properties and methods of a parent class. Here, `Manager` and `Developer` both reuse `Employee` and add their own salary logic.

```python
class Employee:
    def __init__(self, emp_id, name, basic_salary):
        self.emp_id = emp_id
        self.name = name
        self.basic_salary = basic_salary

    def accept(self):
        self.emp_id = int(input("Employee ID: "))
        self.name = input("Name: ")
        self.basic_salary = float(input("Basic Salary: "))

    def display(self):
        print("Employee ID:", self.emp_id)
        print("Name:", self.name)
        print("Basic Salary:", self.basic_salary)

class Manager(Employee):
    def __init__(self, emp_id=0, name="", basic_salary=0, allowance=0, bonus=0):
        Employee.__init__(self, emp_id, name, basic_salary)
        self.allowance = allowance
        self.bonus = bonus

    def accept(self):
        Employee.accept(self)
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
    def __init__(self, emp_id=0, name="", basic_salary=0, overtime_hours=0, overtime_rate=0):
        Employee.__init__(self, emp_id, name, basic_salary)
        self.overtime_hours = overtime_hours
        self.overtime_rate = overtime_rate

    def accept(self):
        Employee.accept(self)
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

A lambda is a small anonymous function written in one line. It is useful for short tasks.

```python
numbers1 = [1, 2, 3, 4]
numbers2 = [5, 6, 7, 8, 9]

squares = list(map(lambda x: x * x, numbers1))
evens = list(filter(lambda x: x % 2 == 0, numbers2))

print(squares)
print(evens)
```

## Q29. What is the difference between mutable and immutable data types in Python? Explain with examples of list, tuple, string, and dictionary. What happens when you try to modify an immutable object?

**Topic to read on W3Schools:** Python Lists, Python Tuples, Python Strings, Python Dictionaries

Mutable means the value can be changed after creation. Immutable means it cannot be changed after creation. Lists and dictionaries are mutable. Tuples and strings are immutable.

```python
my_list = [1, 2, 3]
my_tuple = (1, 2, 3)
my_string = "abc"
my_dict = {"a": 1}

my_list[0] = 10
my_dict["a"] = 20

print(my_list)
print(my_dict)

# my_tuple[0] = 10   # error
# my_string[0] = "z" # error
```

If you try to change an immutable object, Python raises an error.

## Q30. Explain the four pillars of Object Oriented Programming with a real-life example for each. Which pillar is demonstrated by method overriding and why?

**Topic to read on W3Schools:** Python OOP, Python Inheritance, Python Polymorphism, Python Encapsulation

The four pillars are:

Encapsulation: keeping data safe inside a class, like a bank account keeping balance private.  
Inheritance: one class gets features of another class, like a car being a kind of vehicle.  
Polymorphism: one method name works in different ways, like `move()` for a car, boat, and plane.  
Abstraction: showing only important details and hiding the extra work, like using a phone without knowing how the internal circuits work.

Method overriding shows polymorphism because the child class uses the same method name but gives a different result.

## Q31. What is the difference between append(), extend(), and insert() in a Python list? Write a program that demonstrates all three methods and also shows how to remove an element using remove() and pop().

**Topic to read on W3Schools:** Python Lists, Python Lists Methods

`append()` adds one item to the end. `extend()` adds many items to the end. `insert()` adds an item at a fixed position. `remove()` deletes by value. `pop()` removes and returns an item by index, usually the last item.

```python
items = [1, 2, 3]

items.append(4)
items.extend([5, 6])
items.insert(1, 10)

print(items)

items.remove(10)
print(items)

last_item = items.pop()
print(last_item)
print(items)
```

## Q32. What is the difference between raise, try, except, else, and finally in Python exception handling? Write a program that demonstrates all five keywords together with a user-defined exception NegativeAgeError.

**Topic to read on W3Schools:** Python Try...Except, Python Exceptions

`raise` throws an error. `try` holds code that may fail. `except` catches the error. `else` runs only if no error happened. `finally` runs no matter what. A user-defined exception is just your own custom error class.

```python
class NegativeAgeError(Exception):
    pass

try:
    age = int(input("Enter age: "))
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

## Q33. Design a Python class hierarchy for a Bank Account System.

**Topic to read on W3Schools:** Python OOP, Python Inheritance, Python Polymorphism, Python Encapsulation

This question mixes abstract classes, custom exceptions, inheritance, and polymorphism.

```python
from abc import ABC, abstractmethod

class InsufficientFundsError(Exception):
    pass

class Account(ABC):
    def __init__(self, holder_name, balance):
        self.holder_name = holder_name
        self.balance = balance

    def deposit(self, amount):
        self.balance = self.balance + amount

    def withdraw(self, amount):
        if amount > self.balance:
            raise InsufficientFundsError("Not enough balance")
        self.balance = self.balance - amount

    def __str__(self):
        return "Holder: " + self.holder_name + ", Balance: " + str(self.balance)

    @abstractmethod
    def calculate_interest(self):
        pass

class SavingsAccount(Account):
    def calculate_interest(self):
        return self.balance * 0.04

class CurrentAccount(Account):
    def calculate_interest(self):
        return 0

accounts = [SavingsAccount("A", 10000), CurrentAccount("B", 5000)]

i = 0
while i < len(accounts):
    print(accounts[i])
    print(accounts[i].calculate_interest())
    i = i + 1
```

## Q34. Concurrency — AsyncIO vs Threading (Marks: 15)

**Topic to read on W3Schools:** Python Modules, Python Try...Except, Python File Handling

This question is about doing many tasks together.

Threading is good for waiting tasks like network calls or file waiting. Multiprocessing is better for heavy CPU work. AsyncIO is best when many network tasks wait at the same time.

### a) AsyncIO program using aiohttp

```python
import asyncio
import aiohttp

URLS = [
    "https://www.google.com",
    "https://www.python.org",
    "https://www.github.com",
    "https://www.wikipedia.org",
    "https://www.stackoverflow.com"
]

async def fetch_status(session, url):
    try:
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
        i = 0
        while i < len(URLS):
            tasks.append(fetch_status(session, URLS[i]))
            i = i + 1

        results = await asyncio.gather(*tasks)

        i = 0
        while i < len(results):
            print(results[i][0], "->", results[i][1])
            i = i + 1

asyncio.run(main())
```

### b) Compare Threading, Multiprocessing, and AsyncIO

Threading: best for I/O-bound tasks, like downloading files or waiting for network responses. GIL limits CPU work. Memory usage is moderate. Code is easy to medium.

Multiprocessing: best for CPU-bound tasks, like image processing or large calculations. GIL does not block it because each process has its own Python interpreter. Memory usage is higher. Code is a little harder.

AsyncIO: best for many I/O tasks at once, like many web requests. GIL is not the main issue because it uses one thread and event loop. Memory usage is low. Code can feel harder at first.

### c) Thread-safe counter and broken counter

```python
import threading

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

safe_threads = []
unsafe_threads = []

i = 0
while i < 100:
    t1 = threading.Thread(target=safe_worker)
    t2 = threading.Thread(target=unsafe_worker)
    safe_threads.append(t1)
    unsafe_threads.append(t2)
    t1.start()
    t2.start()
    i = i + 1

i = 0
while i < 100:
    safe_threads[i].join()
    unsafe_threads[i].join()
    i = i + 1

print("Safe count:", safe_count)
print("Unsafe count:", unsafe_count)
```

### d) What is the GIL?

The GIL means Global Interpreter Lock. In CPython, it allows only one thread to execute Python bytecode at a time. Python has it mainly to make memory management simpler and safer. A big bottleneck happens in CPU-heavy thread programs, because threads cannot truly run Python code in parallel. Multiprocessing is not affected in the same way because each process has its own Python interpreter and its own GIL.

## Q35. Generators and Iterators

**Topic to read on W3Schools:** Python Generators, Python Iterators, Python File Handling

A generator gives one value at a time and saves memory. An iterator is an object that returns values one by one when used in a loop.

### a) read_errors(filename)

```python
def read_errors(filename):
    f = open(filename, "r")
    for line in f:
        if "ERROR" in line:
            yield line.strip()
    f.close()
```

A generator is better than `readlines()` here because `readlines()` loads the whole file into memory, but a generator gives one line at a time.

### b) parse_errors(lines)

```python
def parse_errors(lines):
    for line in lines:
        parts = line.split(" ", 3)
        if len(parts) == 4:
            record = {
                "timestamp": parts[0] + " " + parts[1],
                "level": parts[2],
                "message": parts[3]
            }
            yield record

parsed = parse_errors(read_errors("server.log"))

i = 0
for item in parsed:
    print(item)
    i = i + 1
    if i == 3:
        break
```

### c) Fibonacci using generator and custom iterator

```python
def fibonacci_generator(n):
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

print("Generator:")
for x in fibonacci_generator(5):
    print(x)

print("Iterator:")
for x in FibonacciIterator(5):
    print(x)
```

## Final note

The topic labels above are mapped to the matching W3Schools Python pages such as Functions, Class Properties, Class Methods, Inheritance, Polymorphism, Try...Except, Generators, Lambda, RegEx, File Handling, Pandas, NumPy, and OOP. citeturn121973search7turn121973search2turn121973search3turn954471search4turn954471search0turn954471search2turn954471search6turn121973search0