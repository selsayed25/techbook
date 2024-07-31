---
title: "Python Object-Oriented Programming"
weight: 2
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# Python Object-Oriented Programming

Object-Oriented Programming (OOP) is all about organizing your code into "objects," which are like real-world entities that bundle together data and behaviors. Python, being a versatile language, supports OOP features that make it easier to create clean, modular, and reusable code.

## A Bit of History

The concept of OOP was first introduced by Alan Kay in the 1960s with the Smalltalk language. Smalltalk was revolutionary, bringing forward ideas like classes, objects, inheritance, and polymorphism. Fast forward to the late 1980s, and Guido van Rossum designed Python with readability and simplicity in mind. Python embraced OOP principles, making it a great choice for both beginners and seasoned developers who want to write clear and effective code.

Over the years, Python has evolved, with significant updates in both Python 2.x and Python 3.x that enhanced its OOP capabilities. Its flexible and dynamic nature continues to make it a favorite for learning and applying OOP.

## Classes and Objects

### What Are They?

In Python, a class acts like a blueprint for creating objects. It defines the attributes (data) and methods (behaviors) that the objects will have. An object is essentially an instance of a class, carrying its own data and able to use the methods defined by its class.

Let’s look at a simple example of defining a class and creating an object:

```python
# Define a class
class Dog:
    def __init__(self, name, age):
        self.name = name  # Attribute for the dog's name
        self.age = age    # Attribute for the dog's age

    def bark(self):
        return f"{self.name} says Woof!"

# Create an object (instance) of the class
my_dog = Dog(name="Buddy", age=3)

# Access attributes and methods
print(my_dog.name)  # Output: Buddy
print(my_dog.bark())  # Output: Buddy says Woof!
```

In this example, the `Dog` class has an `__init__` method that sets up the dog's name and age. The `bark` method provides behavior for the `Dog` objects. We create an instance called `my_dog` and use it to access its attributes and call its methods.

### Methods and Attributes

Methods are functions inside a class that describe the behaviors of an object, while attributes are variables that store data about the object.

Here’s an example showing both instance methods and class attributes:

```python
class Car:
    wheels = 4  # Class attribute, shared by all Car instances

    def __init__(self, make, model):
        self.make = make  # Instance attribute
        self.model = model  # Instance attribute

    def display_info(self):
        return f"{self.make} {self.model} with {Car.wheels} wheels"

# Create an object (instance) of the class
my_car = Car(make="Toyota", model="Camry")

# Access methods and attributes
print(my_car.display_info())  # Output: Toyota Camry with 4 wheels
```

Here, `wheels` is a class attribute shared across all `Car` instances, while `make` and `model` are specific to each `Car` object. The `display_info` method shows how both types of attributes can be used.

### Inheritance

Inheritance allows you to create new classes based on existing ones. It helps you reuse code and create a hierarchy of classes. The base class is the one being inherited from, and the derived class is the one that inherits.

Here’s a simple example of inheritance:

```python
# Base class
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "Animal sound"

# Derived class
class Cat(Animal):
    def speak(self):
        return f"{self.name} says Meow!"

# Create an object (instance) of the derived class
my_cat = Cat(name="Whiskers")

# Access inherited and overridden methods
print(my_cat.speak())  # Output: Whiskers says Meow!
```

In this example, `Cat` inherits from `Animal` and overrides the `speak` method to provide a specific sound for cats. The `Cat` class also inherits the `__init__` method from `Animal`.

### Polymorphism

Polymorphism means that different classes can be treated as instances of the same class through a common interface. It allows methods to operate differently depending on the object’s class.

Here’s how polymorphism works:

```python
class Bird:
    def speak(self):
        return "Bird sound"

class Dog:
    def speak(self):
        return "Woof!"

def make_it_speak(animal):
    print(animal.speak())

# Create objects of different classes
my_bird = Bird()
my_dog = Dog()

# Use polymorphism to call the same method on different objects
make_it_speak(my_bird)  # Output: Bird sound
make_it_speak(my_dog)   # Output: Woof!
```

In this example, the `make_it_speak` function uses polymorphism to call the `speak` method on different objects. Even though `speak` behaves differently in `Bird` and `Dog`, the function handles both seamlessly.

## Encapsulation

Encapsulation is about bundling data and methods that work on that data into a single unit (class) and controlling access to it. It helps protect an object's state from unintended interference.

In Python, we use naming conventions to indicate access levels. For example, attributes starting with a single underscore `_` are protected, while those with a double underscore `__` are private.

Here’s how encapsulation works in Python:

```python
class BankAccount:
    def __init__(self, account_number, balance):
        self.__account_number = account_number  # Private attribute
        self.__balance = balance  # Private attribute

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def withdraw(self, amount):
        if amount > 0 and amount <= self.__balance:
            self.__balance -= amount

    def get_balance(self):
        return self.__balance

# Create an object (instance) of the class
account = BankAccount(account_number="123456", balance=1000)

# Access methods to modify and retrieve the balance
account.deposit(500)
print(account.get_balance())  # Output: 1500

# Direct access to private attributes is restricted
# print(account.__balance)  # AttributeError: 'BankAccount' object has no attribute '__balance'
```

In this example, the `BankAccount` class uses private attributes to keep the account number and balance safe from direct manipulation. Methods like `deposit`, `withdraw`, and `get_balance` provide controlled access to these attributes.

## Abstract Classes and Interfaces

Abstract classes are templates that can’t be instantiated on their own but are meant to be extended by other classes. They often include abstract methods, which must be implemented by subclasses. Python uses the `abc` module to handle abstract classes.

Here’s an example:

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

    def perimeter(self):
        return 2 * (self.width + self.height)

# Create an object (instance) of the derived class
rect = Rectangle(width=5, height=3)

# Access methods
print(rect.area())       # Output: 15
print(rect.perimeter())  # Output: 16
```

In this example, `Shape` is an abstract class with abstract methods `area` and `perimeter`. The `Rectangle` class implements these methods, providing the specific details for rectangles.

## Composition

Composition involves creating classes that contain objects of other classes, rather than inheriting from them. This approach is often more flexible and modular.

Here’s how composition works:

```python
class Engine:
    def start(self):
        return "Engine started"

class Car:
    def __init__(self, engine):
        self.engine = engine

    def start(self):
        return self.engine.start() + " and Car started"

# Create an Engine object
engine = Engine()

# Create a Car object with the Engine object
my_car = Car(engine=engine)

# Access methods
print(my_car.start())  # Output: Engine started and Car started
```

In this example, the `Car` class uses composition to include an `Engine` object. This design allows the `Car` class to use the engine's functionality without being tightly coupled to it.