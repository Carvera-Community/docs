---
description: Keyboard Shortcuts settings were added in version 2.3.0
---

# Keyboard Shortcuts

All keyboard shortcuts in the Controller can be viewed and reassigned in **Settings → Keyboard Shortcuts**.

Shortcuts are grouped into three contexts:

| Context | When active |
| --- | --- |
| **Global** | Any time the application has focus |
| **Jogging** | Only while Keyboard Jogging is enabled |
| **MDI** | Only while the MDI text box has focus |

## Default Bindings

### Global

| Action | Default |
| --- | --- |
| Open Online Documentation | F1 |
| Open Settings | Cmd+, (macOS) / Ctrl+, |
| Open / Focus MDI | Ctrl+M |
| Open / Focus G-Code | Ctrl+G |
| Open File Browser | Ctrl+O |
| Toggle Keyboard Jogging | Ctrl+J |
| Switch Jog Mode | Ctrl+K |
| Open Start Job | _Unbound_ |

### Jogging

| Action | Default |
| --- | --- |
| Jog X+ | Right Arrow |
| Jog X− | Left Arrow |
| Jog Y+ | Down Arrow |
| Jog Y− | Up Arrow |
| Jog Z+ | Page Up |
| Jog Z− | Page Down |
| Jog A+ | _Unbound_ |
| Jog A− | _Unbound_ |

{% hint style="info" %}
When the **Invert Y-Axis Jogging Buttons** setting is enabled, the default Y+ and Y− keys are swapped so Up moves the spindle away and Down moves it toward the user.
{% endhint %}

### MDI

| Action | Default |
| --- | --- |
| Send Command | Ctrl+Enter |
| Insert New Line | Enter |

{% hint style="info" %}
Not currently configurable are the key short cuts to recall past MDI command history (up/down arrow keys), and selecting a Intellisense command suggestion (tab).
{% endhint %}

## Customising a Shortcut

1. Open **Settings -> Keyboard Shortcuts**.
2. Click the key binding you want to change.
3. Press the new key combination. The recorder captures modifier keys (Ctrl, Alt, Shift, Cmd/Meta) together with one non-modifier key.
4. If the new combination conflicts with another shortcut in the same or overlapping context, a warning is shown and the change is blocked until the conflict is resolved.
5. Click **Reset** next to any binding to restore its default, or **Reset All** to restore every shortcut.

Customised bindings are saved automatically and persist across Controller restarts.

## Platform Modifier

The **Primary** modifier resolves to **Cmd** on macOS and **Ctrl** on Windows and Linux. Default shortcuts that use Primary will display the platform-appropriate key in the UI.
