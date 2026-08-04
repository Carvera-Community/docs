---
description: Connection and protocol autodetection was added in version 2.2.0
---

# Connection & Communication Protocol

How the Controller talks to the machine over WiFi or USB.

## Protocol autodetection

Firmware may use **Makera** (framed) or **Smoothie** (newline) protocol. On connect the Controller detects which is active and uses it for the session. No manual setting is required for normal use.

## USB

* Connection list only shows devices matching Makera USB ids
* Devices are remembered by device identifier, not by COM/tty number
* A progress popup is shown while the port opens
* Higher baud negotiation (when enabled) runs after config sync and works with both protocols
* Sending `reset` over USB is blocked; use the machine power switch instead

## WiFi / network

* **Scan Wi-Fi** includes a **Network…** option to type a machine address manually
* Preferred connection method (USB vs WiFi) is used on fresh app launch when auto-reconnect is enabled
* After a drop, reconnect prefers the **last successful** method

See [Auto-Reconnect](auto-reconnect.md).
