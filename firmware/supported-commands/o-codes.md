---
description: O Codes support was added in version 2.2.0c
---

# O Codes

Community firmware supports a subset of [LinuxCNC O-codes](https://linuxcnc.org/docs/html/gcode/o-code.html) for conditionals, loops, and in-file subroutines. Labels must be uppercase (`O100`, not `o100`). O-codes only run when playing a file — not from MDI.

Examples below use [M118.1](mcodes/printing-text.md#m118.1-p-print-parameter-value) and [variables](../features/variables.md) / [math](../features/math.md) expressions.

## Conditionals

`if` / `elseif` / `else` / `endif`

```gcode
O102 if [#101 lt 3]
  M118.1 P1
O102 elseif [#101 lt 10]
  M118.1 P2
O102 else
  M118.1 P3
O102 endif
```

## Loops

`do` / `while` / `endwhile` / `repeat` / `endrepeat`, plus targeted `break` / `continue` (including breaking an outer loop by label).

```gcode
O500 while [#101 le 10]
  O501 if [#101 gt 3]
    O500 break
  O501 endif
  M118.1 P#101
  #101 = [#101 + 1]
O500 endwhile
```

```gcode
O300 do
  M118.1 P#101
  #101 = [#101 + 1]
O300 while [#101 lt 5]
```

```gcode
O400 repeat [3]
  M118.1 P#101
  #101 = [#101 + 1]
O400 endrepeat
```

## Subroutines

`sub` / `endsub` / `call` / `return` with up to 30 local arguments (`#1`–`#30`). Arguments are restored when the subroutine returns. User variables `#101`–`#120` are not.

```gcode
O940 sub
  M118.1 P#1
  M118.1 P#2
O940 endsub

#101 = 7
#102 = 3
O940 call [#101 - 2] [#102 * 2]
```

## Playing files with subroutines

By default, subroutine entry points are discovered lazily during playback. Pass `-O` to [`play`](console-commands/README.md) to pre-scan the file up front (also reports pre-scan progress to the controller):

```
play /sd/gcodes/job.nc -O
```

Nesting depth is limited to 10.

## Not supported

* O-codes from MDI
* External file subroutines
* Subroutine return values
* Indirection such as `O[#101+2]`
* Fanuc-style numbered programs (use `call` / `return`, or existing [M98](mcodes/macros.md))
* Lowercase o-code labels
