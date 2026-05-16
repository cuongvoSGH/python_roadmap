# Operations - Theoretical Material

This section teaches how to access and manipulate elements in data structures using indexing, slicing, membership tests, and iteration.

## Indexing

- Access individual elements by position.
- Positions start at 0, not 1.

Example:
```python
invoices = [1001, 1002, 1003]
print(invoices[0])  # 1001 (first element)
print(invoices[1])  # 1002 (second element)
print(invoices[-1])  # 1003 (last element, use -1)
```

### Negative indexing
- `-1`: Last element
- `-2`: Second-to-last element
- Useful for accessing end of list without knowing length.

## Slicing

- Access multiple consecutive elements.
- Use format: `[start:end]`
- Includes start, excludes end.

Example:
```python
amounts = [100, 200, 300, 400, 500]
print(amounts[0:3])  # [100, 200, 300] (first 3 elements)
print(amounts[1:4])  # [200, 300, 400] (elements 1, 2, 3)
print(amounts[:3])   # [100, 200, 300] (from start to index 3)
print(amounts[2:])   # [300, 400, 500] (from index 2 to end)
```

## Dictionary access

- Use keys, not positions.
- Safer than list indexing: returns `None` if not found (with `.get()` method).

Example:
```python
invoice = {"id": 1001, "amount": 250.00, "status": "paid"}
print(invoice["id"])       # 1001
print(invoice.get("id"))   # 1001 (safer method)
print(invoice.get("notes", "No notes"))  # Default if missing
```

## Membership tests

- Check if item exists in collection.
- Use `in` keyword.

Example:
```python
departments = ("Sales", "Finance", "HR")
if "Finance" in departments:
    print("Finance found")

accounts = [101, 102, 103]
if 102 in accounts:
    print("Account exists")
```

## Iteration

- Loop through each element.
- Access elements one at a time.

Example:
```python
invoices = [1001, 1002, 1003]
for invoice in invoices:
    print(invoice)

# Dictionary iteration
customer = {"name": "John", "email": "john@mail.com"}
for key in customer:
    print(f"{key}: {customer[key]}")
```

## Finance examples

### Access transaction amount
```python
transaction = [1001, 250.50, "paid", "2024-12-01"]
print(f"Amount: ${transaction[1]}")
```

### Get recent transactions
```python
all_transactions = [100, 200, 300, 400, 500, 600]
recent = all_transactions[-3:]  # Last 3 transactions
print(recent)  # [400, 500, 600]
```

### Check account type
```python
account_types = ("Checking", "Savings", "Money Market")
user_input = "Savings"
if user_input in account_types:
    print("Valid account type")
else:
    print("Invalid account type")
```

### Process each invoice
```python
invoices = [
    {"id": 1001, "amount": 250},
    {"id": 1002, "amount": 500},
    {"id": 1003, "amount": 750}
]
for invoice in invoices:
    print(f"Invoice {invoice['id']}: ${invoice['amount']}")
```

## Best Practices

1. **Remember indexing starts at 0**: Common source of errors.
2. **Use negative indexing for end elements**: Clearer than calculating position.
3. **Use `.get()` for dictionaries**: Safer than direct access with `[]`.
4. **Check membership before accessing**: Prevent errors.
5. **Use descriptive variable names in loops**: `for invoice in invoices:` is clearer.
6. **Document data structure layout**: Comment what each index or key represents.

## Key Takeaways

- Indexing accesses elements by position (starts at 0).
- Slicing accesses ranges of elements.
- Dictionary access uses keys, not positions.
- Use `in` to check if item exists.
- Iteration processes each element in order.
