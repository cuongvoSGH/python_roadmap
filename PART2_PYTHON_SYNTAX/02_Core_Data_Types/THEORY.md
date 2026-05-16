# Core Data Types - Theoretical Material

This section teaches Python's core data types: integers, floats, strings, booleans, and None. It also covers type conversion, which is crucial for handling financial data.

## Understanding data types

Each value in Python has a type:
- **Integer** (`int`): Whole numbers like 100, -50
- **Float** (`float`): Decimal numbers like 123.45, 99.99
- **String** (`str`): Text like "Invoice", "ABC Corp"
- **Boolean** (`bool`): True or False
- **None**: Represents no value

## Integers

- Whole numbers without decimals.
- Use for counts: invoice numbers, item quantities.
- Example: `invoice_count = 50`

## Floats

- Numbers with decimals.
- Essential in finance for amounts, percentages, rates.
- Example: `interest_rate = 0.05`

**Best practice:** Always use float for financial amounts, even if they appear to be whole numbers (e.g., `amount = 100.00` not `amount = 100`).

## Strings

- Text enclosed in single or double quotes.
- Use for names, descriptions, codes.
- Example: `account_name = "Checking Account"`

## Booleans

- Only two values: `True` or `False`.
- Use for yes/no decisions.
- Example: `is_paid = True`

## None

- Represents the absence of a value.
- Useful when a variable hasn't been set yet.
- Example: `balance = None`

## Type conversion

Convert between types using `int()`, `float()`, `str()`.

Examples:
```python
amount_text = "1500.50"
amount_number = float(amount_text)  # Converts to 1500.5

quantity = 10
quantity_text = str(quantity)  # Converts to "10"

price = "99.99"
price_int = int(float(price))  # Converts to 99
```

## Checking data types

Use `type()` to see what type a value is:
```python
print(type(100))      # <class 'int'>
print(type(100.50))   # <class 'float'>
print(type("Invoice"))  # <class 'str'>
print(type(True))     # <class 'bool'>
```

## Best Practices

1. **Use float for financial amounts**: Always store money as `float`, not `int`.
2. **Be careful with string to number conversion**: Ensure the string contains only numbers.
3. **Check types when reading external data**: Data from Excel or CSV might arrive as strings.
4. **Use bool for conditions**: Clearer than 0 or 1.
5. **Document assumptions**: Make clear which fields are strings vs. numbers.

## Finance example

```python
# Customer transaction data
customer_id = 1001  # int
account_balance = 5000.00  # float (always use float for money)
customer_name = "John Doe"  # str
account_active = True  # bool
previous_balance = None  # None (will be set later)

# Convert data from user input
user_input = "2500.50"
deposit_amount = float(user_input)  # Convert to float

print(f"Customer: {customer_name}")
print(f"Balance: ${account_balance}")
print(f"Deposit: ${deposit_amount}")
```

## Key Takeaways

- Different data types store different kinds of information.
- Financial amounts must use `float`, not `int`.
- Use `type()` to check a value's type.
- Convert between types when necessary.
