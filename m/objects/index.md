---
title: Objects Module
project: vlc-lua-docs
---
Useful VLC objects.


## `player()`
Gets the player item object; equivelant to [vlc.player.item()](/vlc-lua-docs/m/player/#item).

### Return value
A player item object if input exists, otherwise `nil`

----
## `playlist()`
Get the playlist object.

### Return value
Playlist object

----
## `libvlc()`
Get instance of libvlc object.

### Return value
Libvlc object or `nil`

----
## `aout()`
Get the aout object.

### Return value
The aout object or `nil`

----
## `vout()`
Get the vout object.

### Return value
The vout object or `nil`  
VOut has variables "aspect-ratio", "autoscale", "crop", "crop-bottom", "crop-top", "crop-left", "crop-right", "deinterlace", "deinterlace-mode", "sub-margin", "secondary-sub-margin", "zoom"