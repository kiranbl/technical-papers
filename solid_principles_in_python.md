# SOLID Principles in Python

## Introduction

SOLID is a set of five design principles for writing code that is easier to understand, test and change. These principles are especially useful when working with classes. The following examples show each principle in simple Python code.

## Principles and Code Examples

### 1. Single Responsibility Principle (SRP)

A class should have one main responsibility. Here, one class stores an invoice and another prints it.

```python
class Invoice:
    def __init__(self, total):
        self.total = total


class InvoicePrinter:
    def print_invoice(self, invoice):
        print(invoice.total)
```

### 2. Open/Closed Principle (OCP)

Code should allow new behavior without requiring changes to existing working code. We can add a discount by creating a new class.

```python
class Discount:
    def apply(self, price):
        return price


class StudentDiscount(Discount):
    def apply(self, price):
        return price * 0.9
```

### 3. Liskov Substitution Principle (LSP)

A child class should work wherever its parent class is expected, without breaking the program.

```python
class Animal:
    def speak(self):
        return "Sound"


class Dog(Animal):
    def speak(self):
        return "Bark"


def make_sound(animal: Animal):
    return animal.speak()


print(make_sound(Dog()))  # Bark
```

### 4. Interface Segregation Principle (ISP)

Classes should not be forced to support methods they do not need. A basic printer only needs printing features.

```python
class Printer:
    def print_file(self):
        print("Printing")


class Scanner:
    def scan_file(self):
        print("Scanning")


class BasicPrinter(Printer):
    pass
```

### 5. Dependency Inversion Principle (DIP)

High-level code should depend on a shared interface instead of a specific implementation. The notifier can work with any sender that follows `Sender`.

```python

class Database:
    def get_data(self):
        return "Database Data"


class API:
    def get_data(self):
        return "API Data"


class FrontEnd:
    def __init__(self, source):
        self.source = source

    def display(self):
        print(self.source.get_data())


FrontEnd(Database()).display()
FrontEnd(API()).display()
```

## Conclusion

SOLID encourages small responsibilities, safe extensions, reliable inheritance, focused interfaces, and flexible dependencies. Applying these ideas where they are useful can make Python projects easier to maintain.

## References

* [Real Python: SOLID Design Principles](https://realpython.com/solid-principles-python/)
