# Refactoring and Avoiding Duplicate Code

---

## 1. Introduction

**Refactoring** is the disciplined process of restructuring existing code without altering its external behavior. The primary goal is to improve code readability, reduce structural complexity, and eliminate duplication (technical debt), making software easier to maintain, test, and extend over time.

---

## 2. The DRY Principle

**DRY** stands for **"Don't Repeat Yourself."** Every piece of knowledge or logic must have a single, unambiguous representation within a codebase.

### Anti-Pattern: Duplicated Logic

```python
def calculate_employee_payout(hours, hourly_rate):
    gross_pay = hours * hourly_rate
    tax_deduction = gross_pay * 0.20
    net_pay = gross_pay - tax_deduction
    print(f"Gross: ${gross_pay:.2f}, Tax: ${tax_deduction:.2f}, Net: ${net_pay:.2f}")
    return net_pay

def calculate_contractor_payout(hours, hourly_rate):
    gross_pay = hours * hourly_rate
    tax_deduction = gross_pay * 0.20
    net_pay = gross_pay - tax_deduction
    print(f"Gross: ${gross_pay:.2f}, Tax: ${tax_deduction:.2f}, Net: ${net_pay:.2f}")
    return net_pay
```

### Refactored: Single Reusable Function

```python
def calculate_payout(hours: float, hourly_rate: float, tax_rate: float = 0.20) -> float:
    """Calculate gross pay, applicable tax, and net payout."""
    gross_pay = hours * hourly_rate
    tax_deduction = gross_pay * tax_rate
    net_pay = gross_pay - tax_deduction
    print(f"Gross: ${gross_pay:.2f}, Tax: ${tax_deduction:.2f}, Net: ${net_pay:.2f}")
    return net_pay

# Usage
employee_net = calculate_payout(40, 25.0)
contractor_net = calculate_payout(40, 50.0, tax_rate=0.15)
```

**Output:**

```text
Gross: $1000.00, Tax: $200.00, Net: $800.00
Gross: $2000.00, Tax: $300.00, Net: $1700.00
```

---

## 3. Essential Refactoring Techniques

### 3.1 Extract Function
When a function is too long or handles multiple concerns, extract cohesive chunks into dedicated helper functions.

```python
# Before
def process_user_registration(user_data):
    if not user_data.get("email") or "@" not in user_data["email"]:
        raise ValueError("Invalid email")
    if len(user_data.get("password", "")) < 8:
        raise ValueError("Password too short")
    print(f"Creating user account for {user_data['email']}")

# After
def validate_registration_data(user_data: dict) -> None:
    if not user_data.get("email") or "@" not in user_data["email"]:
        raise ValueError("Invalid email")
    if len(user_data.get("password", "")) < 8:
        raise ValueError("Password too short")

def process_user_registration(user_data: dict) -> None:
    validate_registration_data(user_data)
    print(f"Creating user account for {user_data['email']}")
```

### 3.2 Extract Variable / Constant
Replace magic literals and complex compound expressions with self-documenting identifiers.

```python
# Before
if order_total * 1.0825 - discount > 500:
    apply_free_express_shipping()

# After
SALES_TAX_RATE = 0.0825
FREE_SHIPPING_THRESHOLD = 500

total_with_tax = order_total * (1 + SALES_TAX_RATE)
final_price = total_with_tax - discount

if final_price > FREE_SHIPPING_THRESHOLD:
    apply_free_express_shipping()
```

### 3.3 Guard Clauses (Early Return)
Replace deep pyramid nesting with quick exit statements.

```python
# Before (Nested)
def process_payment(account, amount):
    if account is not None:
        if account.is_active:
            if account.balance >= amount:
                account.balance -= amount
                return True
            else:
                return False
        else:
            return False
    else:
        return False

# After (Guard Clauses)
def process_payment(account, amount) -> bool:
    if account is None or not account.is_active:
        return False
    if account.balance < amount:
        return False

    account.balance -= amount
    return True
```

---

## 4. Common Code Smells & Solutions

| Code Smell | Description | Recommended Refactoring |
|---|---|---|
| **Duplicated Code** | Similar logic repeated in multiple places | Extract Function or base class |
| **Long Method** | A function spanning over 30-40 lines | Extract smaller, focused functions |
| **Magic Numbers** | Unexplained numeric or string literals | Extract named Constants |
| **Deep Indentation** | 4+ nested levels of `if`/`for` loops | Guard clauses, early returns |
| **Long Parameter List** | Functions taking more than 4 arguments | Group into dataclass or config object |
| **Dead Code** | Unused variables, imports, or functions | Remove immediately |

---

## 5. Best Practices

1. **Write unit tests first:** Always establish a passing test suite before refactoring to verify behavior remains unchanged.
2. **Refactor in micro-steps:** Make one small change, run your tests, commit, and then proceed.
3. **Follow the Rule of Three:** If you write the same logic twice, keep note; the third time, refactor into an abstraction.
4. **Separate refactoring from feature work:** Never add new business features and refactor existing code in the same Git commit.
5. **Apply the Boy Scout Rule:** Leave the codebase cleaner than you found it on every checkout.
