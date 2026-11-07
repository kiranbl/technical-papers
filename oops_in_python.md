# Object-Oriented Programming (OOP) in Python

## Introduction

Object-oriented programming (OOP) is a way to organize Python code using classes and objects. A class is a blueprint, while an object is an instance of that class. OOP is useful when data and related actions belong together. Its four main concepts are:

* **Encapsulation:** Keep data and the methods that manage it in one class.
* **Abstraction:** Show important features while hiding unnecessary details.
* **Inheritance:** Create a new class based on an existing class.
* **Polymorphism:** Use the same method name with different objects.

## Code Examples

### 1. Encapsulation

The `BankAccount` class manages its balance through methods instead of allowing direct changes.

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount > 0:
            self.__balance += amount

    def check_balance(self):
        return self.__balance


account = BankAccount(500)
account.deposit(200)
print(account.check_balance())  # 700
```

### 2. Abstraction, Inheritance and Polymorphism

`Shape` defines a common method. `Square` and `Rectangle` inherit from it and calculate their areas differently.

```python
from abc import ABC, abstractmethod


class Shape(ABC):
    @abstractmethod
    def area(self):
        pass


class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side * self.side


class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height


for shape in [Square(4), Rectangle(3, 5)]:
    print(shape.area())  # 16, then 15
```

## Conclusion

OOP helps make code easier to organize and reuse. Each class should have a clear purpose and its methods should describe what its objects can do.

## References

* [Python Documentation: Classes](https://docs.python.org/3/tutorial/classes.html)
