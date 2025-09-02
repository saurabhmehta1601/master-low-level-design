# SOLID DESIGN PRINCIPLES

# Single Responsibility Principle

> A class should fulfill only single responsibility meaning a class should have a single reason to change.

Benefits:

* Avoid turning classes into God classes and therefore results in focused modules which are easier to maintain.
* Code is more modular and reusable
* Reduced coupling ensures limits ripple effects.
* Helps with collaboration and parallel development.
* Fewer responsibilities meaning fewer changes of bugs
* Easy to test and debug


#### ❌ BAD PRACTICE

```python
class FileManager:
    def read(): pass
    def write(): pass
    def compress(): pass
    def decompress(): pass
```

####  ✅ GOOD PRACTICE

```python
class Filestore:
    def read(): pass
    def write(): pass

class FileCompressor:
    def compress(): pass
    def decompress(): pass
```


## Open Closed

> A class should be open for extension but closed for modification.

A class code should be able to extend but should not be modified unless needed.

Benefits:
* Existing code remains untouched and therefore does not break
* Code is modular, more reusable and testable.
* Adhering to this principle makes it easier to uphold Single Responsibility principle


### ❌ BAD PRACTICE

```python

class PaymentService:

    def pay(self, payment_mode):

        if payment_mode == "CreditCard":
            print("Making payment for Credit Card" )
        if payment_mode == "DebitCard":
            print("Making payment for Debit Card" )
        if payment_mode == "UPI":
            print("Making payment for UPI" )
```

### ✅ GOOD PRACTICE

```python

class PaymentProcessor:
    def pay(): pass

class CreditCardPaymentProcessor(PaymentProcessor):
    def pay(): 
        print("Paying with credit card")

class CreditCardPaymentProcessor(PaymentProcessor):
    def pay(): 
        print("Paying with debit card")

class UPIPaymentProcessor(PaymentProcessor):
    def pay(): 
        print("Paying with UPI")


class PaymentService:
    def pay(self, payment_processor: PaymentProcessor):
        payment_processor.pay()
```

## Liskov Substitution

> Objects of a child should be directly replacable with objects of parent class without breaking the correctness of the program.

This principle is achieved by not forcing the child class to implement functionality that it does not require meaning the the parent class interface should have the smallest possible methods that are actually needed.
Should  split the large interfaces into smaller

### ❌ BAD CODE

```python

class FileManager:
    def read(): pass
    def write() pass


class ReadOnlyFile(FileManager):
    def read():
        print("Reading file...")
    
    def write():
        raise ImplementationError("CAnnot implement write functionality for read  only file")
```

### GOOD PRACTICE

```python

class Readable:
    def read()

class Writeable:
    def  write()

class ReadOnlyFile(Readable):
    def read()
        print("Reading file...")
```