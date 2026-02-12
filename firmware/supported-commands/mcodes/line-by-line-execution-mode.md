# Line-by-Line Execution Mode

## Demonstration of Line by Line Execution

{% embed url="https://youtu.be/28P2BoFFpco?t=204" %}

## M336 - Enable Line-by-Line Execution Mode

### Description

M336 enables line-by-line execution mode. When enabled, the system will pause after every valid G-code line during file playback, skipping empty and commented lines.

### Parameters

None

### Example

```
M336                 ; Enable line-by-line execution mode
```

## M335 - Disable Line-by-Line Execution Mode

## Description

M335 disables line-by-line execution mode. When disabled, the system will execute G-code continuously without pausing between lines.

## Parameters

None

### Example

```
M335                 ; Disable line-by-line execution mode
```

<br>
