# Decorators 101

## What is a decorator ?
In python, everything is object. So; functions are objects too.

A decorator is a function:
 - It take another function as first parameter.
 - It return a *wrapper function* that encapsulate the given function.
 - This wrapper can be written to modify the behavior of the given function.

A function can be decorated (called within a decorator) with this syntax:
```Python
@decorator_function
def my_function():
    # Do things
```
## Writing a basic decorator:

This is a basic decorator example. It doesn't allow to pass paramters.
**Important:** *@decorator_function* is a syntax that allow us to call a decorated version of *common()*.

```Python

# Decorator function: First parameter must be a function.
def decorator_function(function):
    """A decorator function: It return a wrapper function that encapsulate your function, and allow to modify its behavior"""

    def wrapper():
        print("I'm a decorator function, I can do something before")
        function()
        print("I'm a decorator function, I can do something after")
    
    # Return the function Object. We don't call it !
    return wrapper

@decorator_function
def common():
    """A common function. Can be any function in your code. We just add @decorator_function tp decorate it."""
    print("I'm a normal function that print a message.")

# So we can call common like this:
common()

```

## bad ways to call a decorated *common()* without the *@* synthax:
```Python

# First way
decorator_function(common)()

# Second way
common = decorator_function(common)
common()
```
