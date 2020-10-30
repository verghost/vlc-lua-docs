---
title: Messages Module
project: vlc-lua-docs
---
Output text to the messages window (*Tools*->*Messages* or Ctrl+M).

# Availability

| Script Types |
| ------------ |
| All Types |

----
## `info()`
Information messages; displayed with `_lua info:_`.  
Visible at any verbosity.

### Parameters
- `msg` String: text to output to messages window.

----
## `err()`
Error messages; displayed with `_lua error:_`.  
Visible at any verbosity.

### Parameters
- `msg` String: text to output to messages window.

----
## `dbg()`
Debug messages; displayed with `_lua debug:_`.  
Visible at verbosity: 2.

### Parameters
- `msg` String: text to output to messages window.

----
## `warn()`
Warning messages; displayed with `_lua warning:_`.  
Visible at verbosity: 1 or higher.

### Parameters
- `msg` String: text to output to messages window.
