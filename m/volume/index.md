---
title: Volume Module
project: vlc-lua-docs
---
Handle VLC media volume.

# Availability

| Script Types |
| ------------ |
| [Extension](../../t/extensions), [Interface](../../t/intf) |

----
## `get()`
Get the volume level of the player.

### Return value
Number value between 0 and 512 indicating the current volume level (negative value on failure)

----
## `set()`
Set volume of the player.

### Parameters
- `volume` Integer indicating new volume level; between 0 and 1024 (256 is 100% volume)

### Return value
Two values:
- `code` Integer value 0 on success, VLC error code on failure
- `message` "no error" on success, otherwise an error string specifying the type of error

----
## `up()`
Increase the volume of the player.

### Parameters
- `steps` Integer indicating the number of steps to increase the volume by (value of each step is 32)

### Return value
Number value indicating new volume level (will return 0 if unsuccessful)

----
## `down()`
Decrease the volume of the player.

### Parameters
- `steps` Integer indicating the number of steps to decrease the volume by (value of each step is 32)

### Return value
Number value indicating new volume level (will return 0 if unsuccessful)