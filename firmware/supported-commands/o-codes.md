# O Codes

The community firmware has support for a subset of [LinuxCNC O-codes](https://linuxcnc.org/docs/html/gcode/o-code.html).

Text from: [https://github.com/Carvera-Community/Carvera\_Community\_Firmware/pull/323](https://github.com/Carvera-Community/Carvera_Community_Firmware/pull/323)\
\
What is supported:

* Conditionals (`if` / `elseif` / `else` / `endif`):

```gcode
O102 if [#101 lt 3]
  M118.1 P1
O102 elseif [#101 lt 10]
  M118.1 P2
O102 else
  M118.1 P3
O102 endif
```

* Loops (`do` / `while` / `endwhile` / `repeat` / `endrepeat` / targeted `break` / `continue`)

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

* In-file subroutines (`sub` / `endsub` / `call` / `return`) with up to 30 local args

```gcode
O940 sub
  M118 sub expr args:
  M118.1 P#1
  M118.1 P#2
O940 endsub

; Prints 5, 6
#101 = 7
#102 = 3
O940 call [#101 - 2] [#102 * 2]
```

What is not supported yet:

* Using O-codes through the MDI: it'll only work when playing a file
* External files subroutines
* Subroutines return values: I don't think it would be that hard to implement but I'd prefer to validate that this version is working fine before adding other things
* Indirections (ex: `O[#101+2]`): we could probably support the ones used with `call` quite easily
* Fanuc-style numbered program: we already have an M98 that works a bit differently + I don't think the added complexity would be worth it since it basically does the same thing as `call`/`return`
* Lowercase o-codes labels (ex: o100 instead of O100) so it stays coherent with currently supported g-codes/m-codes being uppercase only

Some implementation notes:

* it mainly relies on a new `OCodeHandler` that intercepts all o-prefixed lines in the `Player` before the normal G-code dispatch.
* subroutine entrypoints are stored into a table that is built in a pre-scan phase when opening a file. This pre-scan is disabled by default and requires the `-O` flag to be passed to the `play` command. If the pre-scan is disabled but the file contains some subroutines/calls it will be parsed lazily.
* for other o-codes we either rely on just skipping lines for forward jumps, or a stack for the other ones
* that stack is statically allocated in the AHB pool which takes up a bit of memory but avoids having to handle annoying issues we could have with a dynamic one. It has a max depth of 10.
* the PR adds new variables from `#1` to `#30` that correspond to subroutine parameters. I had to put them into AHBSRAM since simply adding `local_params[30]` to the `Kernel` caused my machine to crash at boot due to memory issues... I also moved user variables into the AHB pool for the sake of consistency, I don't think it should cause any issues.
* the progress tracking is a bit annoying to handle since we can't know prior to execution what will be the total played lines/bytes. As a trade-off I chose to just store the max. value and never go backward. This means that if you have a loop its lines will be considered as having been played after the first execution and the progress will not advance until it is done looping.
* `#1`-`#30` are restored after a subroutine returns, `#101`-`#120` are not (it already takes a lot of memory to handle the first ones)

All the tests present in the `tests/TEST_OCodeFlowControl/TEST_OCodeFlowControl.cnc` file are working properly.
