---
title: OSD Module
project: vlc-lua-docs
---
Utilities to control On-Screen-Display (OSD).


# OSD Elements


## `icon()`
Display an icon on a given OSD channel.

### Parameters
- `type` String value indicating icon type: one of "pause", "play", "speaker" or "mute"
- Optional
	- `id` OSD channel ID; uses default channel if one is not provided

----
## `message()`
Display the text message on a given OSD channel.

### Parameters
- `msg` String containing the message to display
- Optional
	- `id` OSD channel ID; uses default channel if one is not provided
	- `position` String indicating the position of message on the screen: one of "center", "left", "right", "top", "bottom", "top-left", "top-right", "bottom-left" or "bottom-right" (default is "top-right")
	- `duration` Integer indicating the amount of time, in [microseconds](https://en.wikipedia.org/wiki/Microsecond), the message should be displayed (default is 1000000μs = 1 second)

----
## `slider()`
Display slider on a given OSD channel.

### Parameters
- `position` Integer from 0 to 100
- `type` String value: can be either "horizontal" or "vertical" (refers to indicate slider orientaiton)
- Optional
	- `id` OSD channel ID; uses default channel if one is not provided

----
# OSD Channels
Elements are dsiplayed on individual OSD "channels" (a type of Subpicture channel), which can be created or cleared via the OSD module.


## `channel_register()`
Register a new OSD channel.

### Return value
Integer value of new channel ID

----
## `channel_clear()`
Clear a given OSD channel.

### Parameters
- `id` OSD channel ID
