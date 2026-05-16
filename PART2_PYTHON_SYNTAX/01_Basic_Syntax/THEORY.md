# Basic Syntax and Values - Theoretical Material

This section teaches the fundamental building blocks of Python code: comments, variables, and output.

## What are variables?

- A variable is a container that holds a value.
- Think of it like a labeled box where you can store information.
- In finance, you might store an amount like `invoice_amount = 1500.00`.

## Naming variables

Use clear, descriptive names for variables. This makes code easy to understand.

**Good variable names:**
- `total_amount`
- `account_balance`
- `invoice_date`

**Poor variable names:**
- `x`, `y`, `a` (not descriptive)
- `amountinvoice` (hard to read, use underscores)

## Comments

- Comments explain what code does.
- Use `#` to start a comment.
- Comments are ignored when running code.
- Write comments for complex logic or finance-specific calculations.

Example:
```python
# Calculate the total invoice amount
total = 100 + 50
```

## Assigning values

- Use `=` to assign a value to a variable.
- The variable name is on the left, the value on the right.

Example:
```python
amount = 1500
message = "Invoice paid"
is_complete = True
```

## Printing output

- Use `print()` to display values.
- This helps you see the results of your code.
- Useful for checking your work.

Example:
```python
amount = 1500
print(amount)  # Displays: 1500
```

## Best Practices

1. **Use meaningful variable names**: Choose names that describe what the value represents.
2. **Write comments for clarity**: Especially for business logic in finance code.
3. **Keep variables simple**: Store one piece of information per variable.
4. **Print to verify**: Use `print()` to check your calculations are correct.
5. **Use lowercase with underscores**: Follow Python convention (e.g., `invoice_total` not `InvoiceTotal`).

## Example: Finance scenario

```python
# Store invoice details
invoice_number = 1001
amount = 2500.50
payment_status = "Pending"

# Print the information
print(invoice_number)
print(amount)
print(payment_status)
```

## Key Takeaways

- Variables store values in named containers.
- Use clear, descriptive names.
- Comments explain your code.
- `print()` displays values to verify your work.
