# Integer overflow or underflow

### What it does

Checks for integer arithmetic operations which could overflow or panic.
Specifically, checks for any operators (`+`, `-`, `*`, `<<`, etc) which are capable
of overflowing according to the [Rust
Reference](https://doc.rust-lang.org/reference/expressions/operator-expr.html#overflow),
or which can panic (`/`, `%`). No bounds analysis or sophisticated reasoning is
attempted.

### Why is this bad?

Integer overflow will trigger a panic in debug builds or will wrap in
release mode. Division by zero will cause a panic in either mode. In some applications one
wants explicitly checked, wrapping or saturating arithmetic.

### Known problems

### Example

```rust
let a = 0;
let b = a + 1;
```

Use instead:

```rust
let a = 0;
let b = a.checked_add(1).ok_or(Error::OverflowDetected)?;
```

### Implementation

The detector's implementation can be found at [this link](https://github.com/CoinFabrik/scout/tree/main/detectors/integer-overflow-or-underflow).
