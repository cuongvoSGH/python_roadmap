# Loops - Theoretical Material

This section teaches how to repeat code using `for` and `while` loops. Loops are essential for processing multiple transactions, invoices, or records.

## Understanding loops

- A loop repeats code multiple times.
- Use loops instead of copying the same code.
- Two types: `for` loops and `while` loops.

## For loops

- Loop through a collection of items.
- Execute code once for each item.

Example:
```python
invoices = [100, 200, 300]
for amount in invoices:
    print(amount)
```

### Using range() with for loops

- `range()` generates a sequence of numbers.
- `range(5)` generates: 0, 1, 2, 3, 4
- Useful for counting loops.

Example:
```python
for i in range(3):
    print(i)  # Prints: 0, 1, 2
```

## While loops

- Repeat while a condition is `True`.
- Stop when condition becomes `False`.
- Be careful: Make sure the condition will eventually become `False`.

Example:
```python
count = 0
while count < 3:
    print(count)
    count += 1  # Increment to avoid infinite loop
```

## Break and continue

### Break statement
- Stops the loop immediately.
- Use when you find what you're looking for.

Example:
```python
for invoice in [100, 200, 300]:
    if invoice == 200:
        break  # Exit loop when found
    print(invoice)
```

### Continue statement
- Skips to the next iteration.
- Use to skip certain items.

Example:
```python
for amount in [100, 200, 300]:
    if amount == 200:
        continue  # Skip 200
    print(amount)
```

## Finance examples

### Processing transaction list
```python
transactions = [150.50, 200.00, -50.00, 300.25]
total = 0
for amount in transactions:
    total += amount
print(f"Total: ${total}")
```

### Finding specific invoice
```python
invoices = [1001, 1002, 1003, 1004]
target = 1003
for invoice in invoices:
    if invoice == target:
        print(f"Found invoice {invoice}")
        break
```

### Validating all amounts
```python
amounts = [100, 200, 300, -50, 0]
for amount in amounts:
    if amount < 0:
        print(f"Invalid: ${amount}")
        continue
    print(f"Valid: ${amount}")
```

## Best Practices

1. **Use for loops for collections**: When you know the number of iterations.
2. **Use while loops for conditions**: When you don't know when to stop.
3. **Avoid infinite loops**: Always ensure `while` conditions will eventually be `False`.
4. **Use break wisely**: Only when you need to stop early.
5. **Keep loop bodies simple**: Move complex logic to functions.
6. **Use descriptive variable names**: `for invoice_amount in invoices:` is clearer than `for a in list:`.

## Key Takeaways

- `for` loops iterate through collections or ranges.
- `while` loops repeat while a condition is `True`.
- `break` stops a loop.
- `continue` skips to the next iteration.
- Loops process multiple items efficiently.
