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

M118.1 evaluates and prints the value of a specified parameter. This is useful for debugging parameter values during program execution.

### Parameters

* P: Parameter number to evaluate and print (required)

### Example

```
M118.1 P#100        ; Print the value of parameter #100
```
