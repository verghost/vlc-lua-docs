---
title: Windows Module
project: vlc-lua-docs
---
Microsoft Windows specific utilities.  
NOTE: Only available in Widnows builds of VLC.

# Availability

| Script Types |
| ------------ |
| [Extension](../../t/extensions), [Interface](../../t/intf) |

----
## `console_init()`
Initialize the windows console.

----
## `console_wait()`
 Wait for input on the console.

### Parameters
- Optional
	- `timeout` Time, in milliseconds, to wait for input before giving up (default is 0ms)

### Return value
Boolean value: `true` if console input is available, `false` otherwise

----
## `console_read()`
Read input from the windows console (`CONIN$`).  
NOTE: polling and reading from stdin does not work under windows.

### Return value
String containing input read from the console

----
## `console_write()`
Write text output to the windows console (`CONOUT$`).

### Parameters
- `text` String containing the text to be written to the console