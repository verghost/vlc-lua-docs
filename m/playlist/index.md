---
title: Playlist Module
project: vlc-lua-docs
---
Methods to control and manage the VLC playlist.


## `prev()`
Play previous track.

### Usage
```lua
if should_go_back then
	vlc.playlist.prev()
end
```

----
## `next()`
Play next track.

### Usage
```lua
if should_goto_next then
	vlc.playlist.next()
end
```

----
## `skip()`
Skip one or more tracks.

### Parameters
- `num_skips` Integer value: how many tracks to skip

----
## `play()`
Start playback.

----
## `pause()`
Pause playback.

----
## `stop()`
Stop playback.

----
## `clear()`
Clear the playlist.

----
## `repeat()`
Toggle item repeat or set it to a specified value.

### Parameters
- Optional
	- `enable` String value indicating an explicit value to set; 'on' or 'off' (repeat is toggled if no value is passed)

### Return value
Boolean value: `true` if repeat is enabled, `false` otherwise

----
## `repeat_()`
Alias of [repeat()](#repeat), provided since `repeat` is a reserved Lua keyword.

----
## `loop()`
Toggle playlist loop or set it to a specified value.

### Parameters
- Optional
	- `enable` String value indicating an explicit value to set; 'on' or 'off' (loop is toggled if no value is passed)

### Return value
Boolean value: `true` if loop is enabled, `false` otherwise

----
## `random()`
Toggle randomized payback or set it to specified value.

### Parameters
- Optional
	- `enable` String value indicating an explicit value to set; 'on' or 'off' (random playback is toggled if no value is passed)

### Return value
Boolean value: `true` if random playback is enabled, `false` otherwise

----
## `get_repeat()`
Get current repeat mode.

### Return value
Boolean value: `true` if repeat is enabled, `false` otherwise

----
## `get_loop()`
Get current loop mode.

### Return value
Boolean value: `true` if loop is enabled, `false` otherwise

----
## `get_random()`
Get current random mode.

### Return value
Boolean value: `true` if random playback is enabled, `false` otherwise

----
## `goto()`
Go to a specified track in the playlist.  
Provided for Lua <5.0.2

### Parameters
- `id` Integer identifier corresponding to a track in the playlist

### Return value
Two values:
- `code` Integer value 0 on success, VLC error code on failure
- `message` "no error" on success, otherwise an error string specifying the type of error

----
## `gotoitem()`
Alias of [goto()](#goto) provided for all Lua versions.

----
## `add()`
Add one or more items to the playlist, tracks are played when added.

### Parameters
- `...` One or more [playlist items](#playlist-items) to add to the playlist

### Return value
Integer value indicating how many items were added to the playlist

----
## `enqueue()`
Same as [add()](#add), but tracks are not played when added.

----
## `get()`
Get an item from the current playlist.

### Parameters
- `id` Integer value; item identifier

### Return value
The specified [playlist item](#playlist-items)

----
## `list()`
Get list of all playlist items in current playlist.

### Return value
List of all the [playlist items](#playlist-items) in the current playlist

----
## `current()`
Get the ID of the current playlist item.

### Return value
Integer value: identifier of the current playlist item

----
## `current_item()`
Get the current playlist item.

### Return value
The current [playlist item](#playlist-items)

----
## `sort()`
Sort the current playlist according to a given key.

### Parameters
- `key` String containing the sorting key; must be one of: 
	- `id`
	- `title`
	- `title nodes first`
	- `artist`
	- `genre`
	- `random`
	- `duration`
	- `title numeric`
	- `album`

### Return value
Two values that indicate how the sort operation went:
- `code` Integer value 0 on success, VLC error code on failure
- `message` "no error" on success, otherwise an error string specifying the type of error

----
## `status()`
Get the status of the current playlist.

### Return value
String literal value, one of: `"stopped"`, `"started"`, `"playing"`, `"paused"`, `"stopping"`, `"unknown"`

----
## `delete()`
Check if an item is in the current playlist and delete it.

### Parameters
- `id` Integer value; item identifier

### Return value
Two values that indicate how the delete operation went:
- `code` Integer value 0 on success, VLC error code on failure
- `message` "no error" on success, otherwise an error string specifying the type of error

----
## `move()`
Move a playlist item. This operation shifts the target item by one if the current item is before the target.

### Parameters
- `id` Integer value; item identifier
- `target` Integer value; identifier of the item in the target position

### Return value
Two values that indicate how the move operation went:
- `code` Integer value 0 on success, VLC error code on failure
- `message` "no error" on success, otherwise an error string specifying the type of error

----
# Playlist Items

A playlist item can contain the following fields:
- `.path` the item's full path / URL
- `.name` the item's name in playlist (OPTIONAL)
- `.title` the item's Title (OPTIONAL, meta data)
- `.artist` the item's Artist (OPTIONAL, meta data)
- `.genre` the item's Genre (OPTIONAL, meta data)
- `.copyright` the item's Copyright (OPTIONAL, meta data)
- `.album` the item's Album (OPTIONAL, meta data)
- `.tracknum` the item's Tracknum (OPTIONAL, meta data)
- `.description` the item's Description (OPTIONAL, meta data)
- `.rating` the item's Rating (OPTIONAL, meta data)
- `.date` the item's Date (OPTIONAL, meta data)
- `.setting` the item's Setting (OPTIONAL, meta data)
- `.url` the item's URL (OPTIONAL, meta data)
- `.language` the item's Language (OPTIONAL, meta data)
- `.nowplaying` the item's NowPlaying (OPTIONAL, meta data)
- `.publisher` the item's Publisher (OPTIONAL, meta data)
- `.encodedby` the item's EncodedBy (OPTIONAL, meta data)
- `.arturl` the item's ArtURL (OPTIONAL, meta data)
- `.trackid` the item's TrackID (OPTIONAL, meta data)
- `.options` a list of VLC options (OPTIONAL) (e.g. `.options = { "run-time=60" }`)
- `.duration` stream duration in seconds (OPTIONAL)
- `.meta` custom meta data (OPTIONAL) (e.g. `.meta = { ["GVP docid"] = "-5784010886294950089", ["GVP version] = "1.1", Hello = "World!" }`)