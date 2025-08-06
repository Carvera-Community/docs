# Optional Stop Mode

## Demonstration

{% embed url="https://youtu.be/28P2BoFFpco?t=230" %}

## M334 - Enable Optional Stop Mode

### Description

M334 enables optional stop mode. When enabled, M1 commands will pause program execution.

### Parameters

None

### Example

```
M334                 ; Enable optional stop mode
```

## M1 - Optional Stop

### Description

M1 performs an optional stop during program execution. The command will pause execution if optional stop mode is enabled. This is useful for debugging or manual intervention during program execution.

### Parameters

None

### Example

```
M1                    ; Optional stop (pauses if optional stop mode is enabled)
```

## Resuming After M1 Optional Stop

After an M1 command pauses execution (when optional stop mode is enabled), you can resume using one of these methods:

{% tabs %}
{% tab title=" Console Command" %}
This is the primary way to resume from a suspended state.

```
resume
```
{% endtab %}

{% tab title="G-code Command" %}
This is the G-code equivalent of the resume command.

```
M601
```
{% endtab %}

{% tab title="Serial Console Character" %}
Sending the tilde character (\~) via serial console will perform a "safe resume". This is what the [Carvera Controller](broken-reference) does when you use the resume button.

```
~
```
{% endtab %}
{% endtabs %}

### When you resume after an M1:

1. Position Restoration: The system restores the saved XYZ positions and state
2. Before Resume G-code: If configured, executes any `before_resume_gcode`
3. Motion Mode: Restores the previous motion mode (G0/G1/G2/G3)
4. File Playback: Continues playing the G-code file from where it was suspended

### Configuration

You can configure custom G-code to run before resuming by setting:

```
before_resume_gcode M3                 ; Turn the Spindle back on
```



## M333 - Disable Optional Stop Mode

### Description

M333 disables optional stop mode. When disabled, M1 commands will not pause program execution.

### Parameters

None

### Example

```
M333                 ; Disable optional stop mode
```
