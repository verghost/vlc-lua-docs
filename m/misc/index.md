---
title: Miscellaneous Module
project: vlc-lua-docs
---
Disparate assortment of VLC utilities only available in Interface scripts.


## `version()`
Get the VLC version string.

### Return value
The VLC version string

----
## `copyright()`
Get the VLC copyright statement.

### Return value
String containing the VLC copyright statement

----
## `license()`
Get the VLC license.

### Return value
String containing the VLC license

----
## `action_id()`
Get the ID of an action.

### Parameters
- `action` String containing the name of an action

### Return value
Number indicating the ID of the given action

----
## `mdate()`
Get the current date.

### Return value
Number representing the current date in [microseconds](https://en.wikipedia.org/wiki/Microsecond)

----
## `mwait()`
Causes the script to wait until the given date

### Usage
```lua
function Sleep(st) -- seconds
	vlc.misc.mwait(vlc.misc.mdate() + st*1000000)
end
```

### Parameters
- `date` The date to be awaited in [microseconds](https://en.wikipedia.org/wiki/Microsecond)

----
## `quit()`
Quit VLC

