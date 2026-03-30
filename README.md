# Genai_assignment_3
# Assignment 3 – Python Functions, Lambdas & Functional Programming

A hands-on Jupyter Notebook covering core Python concepts: default parameters, recursion, lambda expressions, `map()`, `filter()`, and interactive menu-driven programs.

---

## Prerequisites

- Python 3.x
- Jupyter Notebook or JupyterLab

Install Jupyter if needed:

```bash
pip install notebook
```

Launch the notebook:

```bash
jupyter notebook Assignment3.ipynb
```

---

## How to Run

Run cells **in order from top to bottom** using **Shift + Enter** (or the ▶ Run button). Each task is a self-contained cell. Below is a task-by-task breakdown.

---

### Task 1 — Discount Calculator (Cell 2)

**Run:** Cell 2

**What it does:** Defines `apply_discount(price, discount_percentage=5)` which applies a percentage discount to a price. The discount defaults to 5% if not provided. Raises an error if the discount is outside the valid range (0–60%).

**Key concept:** **Default parameter values** — allows a function to be called with fewer arguments than it defines.

**Test cases to try:**

```python
apply_discount(1000, 10)   # → 900.0  (10% off 1000)
apply_discount(500)        # → 475.0  (default 5% off 500)
apply_discount(200, 0)     # → 200.0  (0% discount, no change)
apply_discount(200, 75)    # → Error: discount > 60%
apply_discount(200, -5)    # → Error: discount < 0%
```

---

### Task 2 — Factorial (Cell 4)

**Run:** Cell 4

**What it does:** Defines `factorial(n)` which computes the factorial of a non-negative integer using an iterative loop. Returns `None` and prints a message for negative inputs.

**Key concept:** **Iterative logic with edge case handling** — uses `range(n, 1, -1)` to multiply downward, and guards against invalid (negative) input.

**Test cases to try:**

```python
factorial(5)    # → 120
factorial(0)    # → 1  (0! is defined as 1)
factorial(1)    # → 1
factorial(7)    # → 5040
factorial(-3)   # → None  (prints error message)
```

---

### Task 3 — GST Calculator with Lambda (Cell 6)

**Run:** Cell 6

**What it does:**
- `apply_gst(price)` adds 18% GST to a price using an inline lambda.
- `apply_dis_gst(price, disc_per, gst_per)` first applies a discount, then applies GST on the discounted price.

**Key concept:** **Lambda expressions** — anonymous single-expression functions (`lambda x: x * 0.18`) used for short, throwaway calculations inside a function.

**Test cases to try:**

```python
apply_gst(100)               # → 118.0
apply_gst(500)               # → 590.0
apply_dis_gst(100, 10, 18)   # → 106.2  (10% off → 90, then +18% GST)
apply_dis_gst(200, 20, 18)   # → 188.16 (20% off → 160, then +18% GST)
```

---

### Task 4 — Bulk GST with `map()` (Cell 8)

**Run:** Cell 8

**What it does:** Applies GST to an entire list of prices at once using `map()` with a lambda function.

**Key concept:** **`map(function, iterable)`** — applies a function to every element of a list and returns a new list. Avoids writing an explicit `for` loop.

**Test cases to try:**

```python
# Default prices list: [100, 250, 400, 1200, 50]
apply_gst(18)    # → [118.0, 295.0, 472.0, 1416.0, 59.0]
apply_gst(5)     # → [105.0, 262.5, 420.0, 1260.0, 52.5]
apply_gst(0)     # → [100.0, 250.0, 400.0, 1200.0, 50.0]  (no tax)
```

---

### Task 5 — Price Filter with `filter()` (Cell 10)

**Run:** Cell 10

**What it does:** Splits a list of prices into two groups — prices above 500 (premium) and prices at or below 500 (budget) — using `filter()`.

**Key concept:** **`filter(function, iterable)`** — keeps only elements for which the function returns `True`. Cleaner and more expressive than a loop with `if` conditions.

**Test cases to try:**

```python
# prices = [100, 250, 400, 1200, 50, 2000, 850]
list(filter(lambda x: x > 500, prices))    # → [1200, 2000, 850]
list(filter(lambda x: x <= 500, prices))   # → [100, 250, 400, 50]

# Try with a different threshold:
list(filter(lambda x: x > 300, prices))    # → [400, 1200, 2000, 850]
```

---

### Task 6 — Combining `map()` and `filter()` (Cell 12)

**Run:** Cell 12

**What it does:** `process_prices(prices)` chains two operations: first applies a 10% discount to all prices using `map()`, then filters out any discounted prices below 300 using `filter()`.

**Key concept:** **Function composition with `map()` + `filter()`** — demonstrates a functional programming pipeline where data flows through transformations step by step.

**Test cases to try:**

```python
process_prices([100, 500, 900, 50, 750])
# After 10% discount: [90.0, 450.0, 810.0, 45.0, 675.0]
# After filtering >300: [450.0, 810.0, 675.0]

process_prices([1000, 200, 600])
# After discount: [900.0, 180.0, 540.0]
# After filtering: [900.0, 540.0]

process_prices([50, 100])
# After discount: [45.0, 90.0]
# After filtering: []  (empty — nothing above 300)
```

---

### Task 7 — Interactive Price Manager (Cell 14)

**Run:** Cell 14

**What it does:** A menu-driven program that lets the user build a list of prices interactively. Supports three operations — add a price, view the average, get the maximum — and loops until the user quits.

**Key concept:** **Modular design with a `while True` loop** — business logic is separated into small helper functions (`add_price`, `get_avg_p`, `get_max_p`), and the main loop handles user input and dispatches to the right function. `try/except` handles invalid (non-numeric) input gracefully.

**How to interact:**

```
Enter your choice: 1   → prompted to enter a price, e.g. 100
Enter your choice: 1   → add another price, e.g. 234
Enter your choice: 1   → add another price, e.g. 143
Enter your choice: 2   → prints: Avg price: 159.0
Enter your choice: 3   → prints: Max price: 234.0
Enter your choice: q   → prints: Exited!!!
```

**Edge cases to test:**

- Enter a negative price after choosing `1` → prints `"Price cannot be -ve"`
- Choose `2` or `3` before adding any prices → prints `"No prices added"`
- Enter letters instead of a number for price → prints `"Invalid input"` (caught by `except`)

---

## Key Concepts Summary

| Task | Concept |
|------|---------|
| 1 | Default parameter values |
| 2 | Iterative loops, edge case handling, returning `None` |
| 3 | Lambda expressions for inline calculations |
| 4 | `map()` for applying a function to every element |
| 5 | `filter()` for selecting elements by condition |
| 6 | Chaining `map()` and `filter()` (functional pipeline) |
| 7 | Modular functions, `while` loop, `try/except`, user input |
