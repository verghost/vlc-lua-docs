---
title: Objects Module
project: vlc-lua-docs
---
Useful VLC objects.


## `player()`
Get the [player](../player/) object. Not to be confused with the [player item object](../player/#item).
NOTE: Pre 4.0.0, this was `vlc.object.input()`

### Return value
A player item object if input exists, otherwise `nil`

----
## `playlist()`
Get the playlist object.

### Return value
Playlist object or `nil`

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
VOut has the following [variables](/vlc-lua-docs/m/var):
- `aspect-ratio`
- `autoscale`
- `crop`
- `crop-bottom`
- `crop-top`
- `crop-left`
- `crop-right`
- `deinterlace`
- `deinterlace-mode`
- `sub-margin`
- `secondary-sub-margin`
- `zoom`