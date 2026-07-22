# Printing Text

## M118 - Print Message

### Description

M118 prints a message to the console. This is useful for debugging, status reporting, or user communication during program execution.

### Parameters

* Text: Any text following the M118 command (required)
* Subcode 1: Special mode for parameter evaluation
* P: Parameter to evaluate and print as result

```
M118 Starting milling job
```

## M118.1 P# - Print Parameter Value

### Description

M118.1 evaluates the expression after **P** and prints it as ` <expression> = <value>`. Expressions such as `#101` or `#101+3` are supported.

### Parameters

* P: Parameter or expression to evaluate (required)

### Example

```
M118.1 P#100        ; Prints:  #100 = 12.000
M118.1 P#101+3      ; Prints:  #101+3 = 15.000
```
