# Data Structures - Theoretical Material

This section teaches how to organize multiple values using lists, tuples, dictionaries, and sets. Choosing the right data structure is crucial for clean, efficient code.

## Overview of data structures

- **List**: Ordered, changeable collection.
- **Tuple**: Ordered, unchangeable collection.
- **Dictionary**: Unordered, key-value pairs.
- **Set**: Unordered collection of unique values.

## Lists

- Use square brackets `[]`.
- Elements are ordered and can be repeated.
- Can be modified: add, remove, change items.

Example:
```python
invoices = [1001, 1002, 1003]
amounts = [100.50, 200.00, 300.25]
descriptions = ["Payment", "Deposit", "Fee"]
```

### When to use lists
- Processing a sequence of similar items.
- Order matters.
- Items may be duplicated.

## Tuples

- Use parentheses `()`.
- Elements are ordered but cannot be changed.
- More memory-efficient than lists.

Example:
```python
months = ("Jan", "Feb", "Mar")
fixed_account_types = ("Checking", "Savings", "Money Market")
```

### When to use tuples
- Data should not change.
- Using as dictionary keys (lists cannot).
- Fixed sets of related items.

## Dictionaries

- Use curly braces `{}` with key-value pairs.
- Keys identify values, like column names in Excel.
- Very flexible and readable.

Example:
```python
invoice = {"id": 1001, "amount": 250.00, "status": "paid"}
account = {"account_number": "12345", "owner": "John Doe", "balance": 5000.00}
```

### When to use dictionaries
- Representing records with named fields.
- Looking up values by name, not position.
- Finance data with multiple related values.

## Sets

- Use curly braces `{}` with unique values.
- No duplicates allowed.
- Fast for checking if item exists.

Example:
```python
account_codes = {"A01", "A02", "A03"}
department_ids = {101, 102, 103}
```

### When to use sets
- Only unique values matter.
- Checking membership quickly.
- Finding common items between groups.

## Choosing the right structure

| Task | Structure |
|------|-----------|
| Process transactions in order | List |
| Fixed accounting periods | Tuple |
| Store invoice with multiple fields | Dictionary |
| Track unique account codes | Set |

## Finance examples

### List for transactions
```python
transactions = [100, -50, 200, 300]
for amount in transactions:
    print(amount)
```

### Dictionary for customer record
```python
customer = {
    "id": 5001,
    "name": "ABC Corp",
    "email": "contact@abc.com",
    "balance": 5000.00,
    "status": "active"
}
print(customer["name"])  # Access by key
```

### Set for unique departments
```python
departments = {"Sales", "Finance", "HR"}
if "Finance" in departments:
    print("Finance department exists")
```

## Best Practices

1. **Choose lists for sequential data**: When order matters or duplicates are expected.
2. **Use dictionaries for records**: Much cleaner than using multiple variables.
3. **Use tuples for immutable data**: Protect data that shouldn't change.
4. **Use sets for uniqueness**: When you only care about distinct items.
5. **Name structures clearly**: `invoice_data` is better than `data`.
6. **Document structure**: Comment what each field represents in dictionaries.

## Key Takeaways

- Lists are ordered and changeable.
- Tuples are ordered and unchangeable.
- Dictionaries use key-value pairs for records.
- Sets contain only unique values.
- Choose the right structure for your task.
