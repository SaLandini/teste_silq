# !
propriedades dos tipos classicos:
- We can ignore duplicate classical annotations: !!τ ≡ !τ
- Classical commutes with tuples: !(τ × τ) ≡ !τ × !τ (analogously for n-tuples with n>2). As a consequence, we also have !(τ × τ) ≡ !(τ × !τ) ≡ !(!τ × τ) ≡ !(!τ × !τ)
- Classical commutes with arrays: !τ[] ≡ (!τ)[] ≡ !(τ[])
- Classical commutes with fixed-length arrays: !τ^n ≡ (!τ)^n ≡ !(τ^n)
- Classical values can be re-interpreted as quantum values: !τ <: τ

# qfree

**Example 1** (not `qfree`): `H` is not `qfree` as it introduces superpositions: It maps |0⟩|0⟩ to 1√2n(|0⟩+|1⟩)12n(|0⟩+|1⟩).

**Example 2**: `X` is `qfree`as it neither introduces nor destroys superpositions: It maps ∑1b=0γb|b⟩∑b=01γb|b⟩ to ∑1b=0γb|1−b⟩∑b=01γb|1−b⟩.

**Example 3**: Logical disjunction (as in `x||y`) is of type `const 𝔹×const 𝔹→qfree 𝔹`, since ORing two values neither introduces nor destroys superpositions.

**Example 4**: Function `myEval` (below) takes a `qfree` function `f` and evaluates it on `false`. Thus, `myEval` itself is also `qfree`.

# mfree

**Example**: Function `myEval` (below) takes a `mfree` function as argument and evaluates it on `false`. Thus, `evaluate` itself is also `mfree`.

```Sliq
def myEvalmfree(f:𝔹→mfree 𝔹)mfree{
  return f(false);
}
```

# const

**Example**: Function `myEval` (below) takes a constant `x` and a function `f` that leaves its first argument `const`:

``` Silq
def myEvalconst(const x:𝔹, f: const 𝔹!→𝔹) {
  return f(x)
}
```

# lifted

**Example**: Function `MyOr` is lifted:

``` Silq
def myOr(x:𝔹, y:!𝔹)lifted{
  return x||y;
}
```

# Types

Silq supports the following types. In this list, n stands for an arbitrary expression of type !ℕ.

- 𝟙 (or 1): The singleton type that only contains element ()

- 𝔹 (or B): Booleans

- ℕ (or N): Natural numbers 0, 1, … (must be classical)

- ℤ (or Z): Integers …, -1, 0, 1, … (must be classical)

- ℚ (or Q): Rational numbers (must be classical)

- ℝ (or R): Reals (must be classical). Simulation semantics are implementation-defined (typically floating point)

- int[n]: n-bit integers encoded in two’s complement

- uint[n]: n-bit unsigned integers

- τ×...×τ (or τ x ... x τ): tuple types, e.g., 𝔹×int[n]

- τ[]: dynamic-length arrays

- τ^n: vectors of length n

- !τ: type τ, but restricted to classical values

- [const] τ×...× [const] τ → [mfree|qfree] τ: functions, optionally annotated as mfree or qfree, whose input types are optionally annotated as const

