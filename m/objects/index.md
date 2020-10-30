---
title: Objects Module
project: vlc-lua-docs
---
Useful VLC objects.

# Availability

| Script Types |
| ------------ |
| [Art](../../t/art), [Extension](../../t/extensions), [Interface](../../t/intf), [Meta Fetcher](../../fetcher), [Meta Reader](../../reader), [Services Discovery](../../sd) |

----
## `player()`
Get the [player](../player/) object. Not to be confused with the [player item object](../player/#item).
NOTE: Pre 4.0.0, this was `vlc.object.input()`

### Usage
```lua
local player_obj = vlc.object.player()
```

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