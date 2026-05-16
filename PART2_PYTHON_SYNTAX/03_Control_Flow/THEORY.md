# Control Flow - Theoretical Material

This section teaches how to make decisions in Python using `if`, `elif`, and `else` statements. Control flow allows your code to take different actions based on conditions.

## Understanding control flow

- Control flow decides which code runs based on conditions.
- Conditions are either `True` or `False`.
- Use comparison operators: `>`, `<`, `==`, `!=`, `>=`, `<=`

## If statements

- `if` executes code only if a condition is `True`.

Example:
```python
amount = 1500
if amount > 1000:
    print("Large amount")
```

## If-else statements

- `if` runs when condition is `True`.
- `else` runs when condition is `False`.

Example:
```python
balance = 500
if balance > 0:
    print("Account has funds")
else:
    print("Account is empty")
```

## If-elif-else statements

- Check multiple conditions in order.
- Use `elif` (else if) for additional conditions.
- `else` catches anything not covered above.

Example:
```python
amount = 0
if amount > 0:
    print("Positive")
elif amount == 0:
    print("Zero")
else:
    print("Negative")
```

## Comparison operators

- `>`: Greater than
- `<`: Less than
- `==`: Equal to
- `!=`: Not equal to
- `>=`: Greater than or equal to
- `<=`: Less than or equal to

## Logical operators

- `and`: Both conditions must be `True`
- `or`: At least one condition must be `True`
- `not`: Reverses the condition

Examples:
```python
if amount > 0 and status == "active":
    print("Valid transaction")

if account_type == "savings" or account_type == "checking":
    print("Standard account")

if not is_closed:
    print("Account is open")
```

## Finance decision-making examples

```python
# Check if invoice is overdue
invoice_date = "2024-11-01"
current_date = "2024-12-15"
if current_date > invoice_date:
    print("Invoice may be overdue")

# Determine account status
balance = 100
minimum_balance = 500
if balance < minimum_balance:
    print("Warning: Low balance")
else:
    print("Balance is healthy")
```

## Best Practices

1. **Keep conditions simple**: Break complex logic into multiple conditions.
2. **Use meaningful variable names**: `is_active`, `has_sufficient_funds` are clearer than `active`, `funds`.
3. **Avoid deep nesting**: Too many nested `if` statements makes code hard to read.
4. **Use elif efficiently**: Check most likely conditions first for better performance.
5. **Add comments**: Explain the business logic behind your conditions.

## Key Takeaways

- Use `if` to execute code conditionally.
- Use `elif` and `else` to handle multiple scenarios.
- Comparison operators test conditions.
- Logical operators combine multiple conditions.
- Keep conditional logic clear and well-organized.
