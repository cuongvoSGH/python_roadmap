# Functions and Modules - Theoretical Material

This section teaches how to create reusable blocks of code (functions) and use Python's built-in libraries (modules) to avoid duplication and leverage existing tools.

## Understanding functions

- A function is a reusable block of code.
- Performs a specific task.
- Can accept inputs and return outputs.
- Like Excel functions: `=SUM(A1:A10)`

## Defining functions

- Use `def` keyword.
- Provide a name and parameters in parentheses.
- Use indentation for the function body.

Basic structure:
```python
def function_name(parameter1, parameter2):
    # Code here
    return result
```

Example:
```python
def add(a, b):
    total = a + b
    return total

result = add(100, 200)
print(result)  # 300
```

## Parameters and arguments

- **Parameters**: Placeholders defined in function definition.
- **Arguments**: Actual values passed when calling function.

Example:
```python
def calculate_tax(amount, rate):  # Parameters
    tax = amount * rate
    return tax

result = calculate_tax(1000, 0.1)  # Arguments
```

## Return values

- Functions can return a result with `return`.
- Caller receives the returned value.
- Function without `return` returns `None`.

Example:
```python
def validate_amount(amount):
    if amount > 0:
        return True
    else:
        return False

is_valid = validate_amount(100)
print(is_valid)  # True
```

## Default parameters

- Provide default values for optional parameters.
- Caller doesn't need to provide all arguments.

Example:
```python
def apply_discount(amount, discount=0.1):
    final_amount = amount * (1 - discount)
    return final_amount

print(apply_discount(100))      # Uses default 0.1
print(apply_discount(100, 0.2)) # Uses provided 0.2
```

## Modules

- Collections of reusable functions and variables.
- Python comes with many built-in modules.
- Import modules to use their code.

Example:
```python
import datetime
today = datetime.date.today()
print(today)  # Current date
```

## Commonly used modules

### datetime
- Work with dates and times.
- Essential for financial records.

Example:
```python
import datetime
today = datetime.date.today()
print(today)
```

### math
- Mathematical functions.

Example:
```python
import math
print(math.sqrt(16))  # 4.0
print(math.ceil(4.3))  # 5
```

### time
- Work with time values.

Example:
```python
import time
print(time.time())  # Current timestamp
```

## Finance function examples

### Calculate net amount after tax
```python
def calculate_net(gross_amount, tax_rate):
    tax = gross_amount * tax_rate
    net = gross_amount - tax
    return net

net_income = calculate_net(5000, 0.2)
print(f"Net: ${net_income}")  # $4000
```

### Validate invoice data
```python
def is_valid_invoice(amount, status):
    if amount > 0 and status == "active":
        return True
    return False

if is_valid_invoice(250, "active"):
    print("Invoice is valid")
```

### Calculate interest
```python
def calculate_interest(principal, rate, years):
    interest = principal * rate * years
    total = principal + interest
    return total

total_amount = calculate_interest(1000, 0.05, 3)
print(f"Total: ${total_amount}")
```

## Best Practices

1. **Give functions descriptive names**: `calculate_tax` better than `calc_t`.
2. **Keep functions focused**: One task per function.
3. **Document your functions**: Add comments explaining parameters and return value.
4. **Use default parameters**: For common values.
5. **Return meaningful values**: Makes debugging easier.
6. **Reuse functions**: Avoid copy-pasting code.
7. **Use modules**: Don't reinvent the wheel.

## Key Takeaways

- Functions are reusable blocks of code.
- Use `def` to define functions.
- Functions can accept parameters and return values.
- Modules provide pre-built functions.
- Organize code into functions for clarity and reusability.
