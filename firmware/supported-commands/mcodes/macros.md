# Macros

## Demonstration of Macro Functionality

{% embed url="https://youtu.be/28P2BoFFpco?t=455" %}

## M97 - Goto Line Number

### Description

M97 is a command that allows you to jump to a specific line number in the currently loaded G-code file. This is useful for debugging, testing specific sections of code, or resuming execution from a particular point in the program.The command will:

* Seek to the beginning of the current file
* Count through the lines until it reaches the specified line number
* Resume execution from that line
* Display a confirmation message showing which line it jumped to

### Parameters

* P (required): The line number to jump to. Must be a positive integer.

### Example

```
M97 P50
```

## M98 - Call Macro

### Description

M98 calls a macro (subroutine) from the current program. The macro is loaded from the /sd/gcodes/macros/ directory and executed. After the macro completes, execution returns to the calling program.

### Parameters

* P: Macro number (required) - specifies which macro file to load
* L: Number of repetitions (optional) - defaults to 1
* Subcode 1: Use quoted filename instead of macro number

### Example

```
M98 P5               ; Call macro 5.cnc once
M98 P10 L3           ; Call macro 10.cnc three times
M98.1 "custom_macro" ; Call macro with custom filename
```

## M98.1 - Call Macro by Path

### Description

M98.1 opens a subprogram by path and returns to the main program when done. It calls a macro (subroutine) using a custom filename instead of a macro number, providing more flexibility than the numbered macro system.

### Parameters

* Quoted filename: The macro filename in quotes (required)
  * Can be a relative path or full path
  * If not starting with /sd/gcodes/, it will be automatically prefixed
* L: Number of repetitions (optional) - must come before the path
  * Defaults to 1 if not specified
  * Must be a positive integer

### Example

```
98.1 "custom_macro.cnc"           ; Call macro once
M98.1 L3 "tool_change.cnc"         ; Call tool_change.cnc three times
M98.1 L2 "macros/calibration.cnc"  ; Call calibration macro twice
M98.1 "/sd/gcodes/macros/my_macro.cnc"  ; Full path specification
```

## M99 - Return from Macro

### Description

M99 returns execution from a macro back to the calling program. This is typically used at the end of macro files to return control to the main program.

### Parameters

None

### Example

```
M99                  ; Return from macro to main program
```
