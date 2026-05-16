# Practical Coding Techniques - Theoretical Material

This section teaches practical techniques for writing robust, maintainable code: list comprehensions, error handling, and file operations.

## List comprehensions

- Concise way to create new lists by filtering or transforming.
- Combines loops and conditions into one line.
- Much more readable than traditional loops.

### Basic list comprehension

Example:
```python
# Traditional approach
numbers = [1, 2, 3, 4, 5]
doubled = []
for num in numbers:
    doubled.append(num * 2)

# List comprehension (cleaner)
doubled = [num * 2 for num in numbers]
print(doubled)  # [2, 4, 6, 8, 10]
```

### With filtering

Example:
```python
# Get only positive amounts
amounts = [100, -50, 200, -30, 300]
positive = [amount for amount in amounts if amount > 0]
print(positive)  # [100, 200, 300]
```

### Finance examples

```python
# Calculate 10% tax on each amount
amounts = [100, 200, 300]
taxes = [amount * 0.1 for amount in amounts]

# Get invoice numbers only from active records
invoices = [
    {"id": 1001, "status": "active"},
    {"id": 1002, "status": "closed"},
    {"id": 1003, "status": "active"}
]
active_ids = [inv["id"] for inv in invoices if inv["status"] == "active"]
```

## Error handling with try-except

- Prevents program crashes from errors.
- Gracefully handles problems.
- Essential for production code.

Basic structure:
```python
try:
    # Code that might cause error
    result = risky_operation()
except:
    # Code to run if error occurs
    print("Error occurred")
```

### Specific exception handling

Example:
```python
try:
    amount_text = "not a number"
    amount = int(amount_text)
except ValueError:
    print("Invalid input: not a number")
except TypeError:
    print("Type error occurred")
```

### With else and finally

Example:
```python
try:
    amount = float(input("Enter amount: "))
except ValueError:
    print("Invalid amount")
else:
    print(f"Amount accepted: ${amount}")
finally:
    print("Processing complete")
```

## File reading and writing

- Read data from CSV, Excel, or text files.
- Write processed data back to files.

### Reading a file

Example:
```python
with open("transactions.csv", "r") as file:
    lines = file.readlines()
    for line in lines:
        print(line)
```

### Writing a file

Example:
```python
with open("report.txt", "w") as file:
    file.write("Account Summary\n")
    file.write("===============\n")
    file.write("Balance: $5000.00\n")
```

### Appending to a file

Example:
```python
with open("log.txt", "a") as file:
    file.write("Transaction recorded\n")
```

## Finance practical examples

### Validate and process user input
```python
try:
    amount = float(input("Enter payment amount: "))
    if amount <= 0:
        print("Amount must be positive")
    else:
        print(f"Processing ${amount}")
except ValueError:
    print("Invalid amount: must be a number")
```

### Filter valid transactions
```python
transactions = [100, -50, 0, 200, -30, 300]

# Keep only positive amounts
valid = [t for t in transactions if t > 0]
print(valid)  # [100, 200, 300]
```

### Read and process invoices
```python
try:
    with open("invoices.txt", "r") as file:
        invoices = file.readlines()
        for invoice in invoices:
            print(f"Processing: {invoice.strip()}")
except FileNotFoundError:
    print("Invoices file not found")
```

## Best Practices

1. **Use list comprehensions for clarity**: When transforming or filtering lists.
2. **Always catch specific exceptions**: Know what error you're catching.
3. **Use try-except for external data**: Files, user input, APIs.
4. **Use `with` for file operations**: Automatically closes files properly.
5. **Add meaningful error messages**: Help users understand what went wrong.
6. **Validate input early**: Check data before processing.
7. **Log errors appropriately**: Record what went wrong for debugging.

## Key Takeaways

- List comprehensions filter and transform lists concisely.
- Try-except blocks prevent crashes from errors.
- File operations read and write data to disk.
- Always validate input and handle errors.
- Write code defensively to handle unexpected situations.
