---
title: Random Module
project: vlc-lua-docs
---
Sources for random data in VLC Lua scripts.


## `number()`
Get a single random number between 0 and 2^31 - 1

### Return value
A random number between 0 and 2^31 - 1

----
## `bytes()`
Get random bytes.

### Parameters
- `size` Integer indicating the number of random bytes to retrieve

### Return value
String containing a random sequence bytes of length `size`