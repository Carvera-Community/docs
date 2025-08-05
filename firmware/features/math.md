# Math

The firmware supports extensive mathematical operations in G-code using expressions enclosed in square brackets `[]`. These expressions can be used in G-code parameters and with the [M118.1 P#](../supported-commands/mcodes/printing-text.md#m118.1-p-print-parameter-value) command to evaluate and print results.

## Basic Arithmetic Operations

#### Operators

* `+`: Addition
* `-`: Subtraction
* `*`: Multiplication
* `/`: Division
* `^`: Exponentiation (power)
* `mod`: Modulo (remainder)

### Examples

```
M118.1 P[1+1]        ; Returns result = 2.000
M118.1 P[5-3]        ; Returns result = 2.000
M118.1 P[4*3]        ; Returns result = 12.000
M118.1 P[10/2]       ; Returns result = 5.000
M118.1 P[2^3]        ; Returns result = 8.000
M118.1 P[7mod3]      ; Returns result = 1.000
```

## Mathematical Functions

#### Trigonometric Functions (angles in degrees)

* `sin[x]`: Sine of x degrees
* `cos[x]`: Cosine of x degrees
* `tan[x]`: Tangent of x degrees
* `asin[x]`: Arcsine of x (returns degrees)
* `acos[x]`: Arccosine of x (returns degrees)
* `atan[x]`: Arctangent of x (returns degrees)

### Examples

```
M118.1 P[sin[45]]    ; Returns result = 0.707
M118.1 P[cos[0]]     ; Returns result = 1
M118.1 P[tan[90]]    ; Returns result = nan
M118.1 P[asin[0.5]]  ; Returns result = 30
M118.1 P[acos[0]]    ; Returns result = 90
```

### Other Mathematical Functions

* `sqrt[x]`: Square root of x
* `abs[x]`: Absolute value of x
* `round[x]`: Round x to nearest integer
* `fix[x]`: Floor function (truncate to integer)
* `fup[x]`: Ceiling function (round up to integer)
* `ln[x]`: Natural logarithm of x
* `exp[x]`: Exponential function (e^x)

#### Examples

```
M118.1 P[sqrt[16]]   ; Returns result = 4.000
M118.1 P[abs[-5]]    ; Returns result = 5.000
M118.1 P[round[3.7]] ; Returns result = 4.000
M118.1 P[fix[3.7]]   ; Returns result = 3.000
M118.1 P[fup[3.2]]   ; Returns result = 4.000
M118.1 P[ln[2.718]]  ; Returns result = 1.000
M118.1 P[exp[2]]     ; Returns result = 7.389
```

## Comparison Operators

Boolean comparisons can be used and will evaluate to 1 (true) or 0 (false):

#### Boolean Comparisons

* `eq`: Equal (with tolerance)
* `ne`: Not equal
* `gt`: Greater than
* `ge`: Greater than or equal
* `lt`: Less than
* `le`: Less than or equal

#### Examples

```
M118.1 P[5eq5]       ; Returns result = 1.000 (true)
M118.1 P[3gt2]       ; Returns result = 1.000 (true)
M118.1 P[2lt5]       ; Returns result = 1.000 (true)
M118.1 P[4le4]       ; Returns result = 1.000 (true)
```

## Logical Operators

Logical Operators can be used and will evaluate to 1 (true) or 0 (false):

#### Boolean Logic

* `and`: Logical AND (both values must be non-zero)
* `or`: Logical OR (at least one value must be non-zero)
* `xor`: Logical XOR (exactly one value must be non-zero)
* `nor`: Logical NOR (both values must be zero)

### Examples

```
M118.1 P[1and1]      ; Returns result = 1.000 (true)
M118.1 P[0or1]       ; Returns result = 1.000 (true)
M118.1 P[1xor0]      ; Returns result = 1.000 (true)
M118.1 P[0nor0]      ; Returns result = 1.000 (true)
```

## Complex Expressions

Complex expressions can be used and will be evaluated per normal PEMDAS order of operations.

#### Order of Operations (PEMDAS)

1. Parentheses/Brackets
2. Exponentiation
3. Multiplication/Division/Modulo
4. Addition/Subtraction
5. Comparison operators
6. Logical operators

#### Examples

```
M118.1 P[1+2*[5-2*2]+2^2+sin[45]]   ; Returns result = 7.707
```

## Error Handling

The follow are the expected behaviors when errors are encountered:

* Division by zero: Halts with error
* Modulo by zero: Halts with error
* Undefined functions: Returns nan
* Invalid variables: Halts with error
* Mismatched brackets: Halts with error

## Further Reading

[GCodeTutor.com](https://gcodetutor.com/cnc-macro-programming/cnc-variables.html) has a good article describing how variables and math can be used in GCode.&#x20;
