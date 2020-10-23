---
title: Player Module
project: vlc-lua-docs
---
###### NOTE: Called "input" pre 4.0; access would be via `vlc.input`.
Used to handle the VLC player interface.


----
# Player Item
This item is an instance of the player class; used to get information on the current player interface and manage metadata.


## `item()`
Constructor for the VLC player item object; gets the current player item.

### Usage
```lua
local player_item = vlc.player.item()
```

### Return value
Object representing the current VLC player item or `nil` if no item is loaded

----
## `item:is_preparsed()`
Determine if item metadata has been preparsed.  
Preparsing loads metadata from files opened with VLC before it is explicitly requested by the user; it is on by default.

### Usage
```lua
local p_item = vlc.player.item()
if not p_item:is_preparsed() then
	print("Preparsing is turned off!")
end
```

### Return value
Boolean value: `true` if metadata has been preparsed, `false` otherwise

----
## `item:metas()`
Get VLC-specific mata data of current item as table. Table keys are only included in the table if values exist.  
Table keys are: 
- `title` 
- `artist` 
- `genre` 
- `copyright` 
- `album` 
- `track_number` 
- `description` 
- `date` 
- `setting` 
- `url` 
- `language` 
- `now_playing` 
- `publisher` 
- `encoded_by` 
- `artwork_url` 
- `track_id` 
- `track_total` 
- `director` 
- `season` 
- `episode` 
- `show_name` 
- `actors` 
- `filename` (Includes file extension)

### Usage
```lua
local p_item = vlc.player.item()
local metas = p_item:metas()
if not (metas == nil) then
	print("Name of current file: " .. metas["filename"])
end
```

### Return value
Table containing the VLC-specific metadata of the current item

----
## `item:set_meta()`
Modify VLC-specific metadata of current item. Does not write new metadata to the actual file.

### Usage
```lua
local p_item = vlc.player.item()
p_item:set_meta("album", "new album name")
```

### Parameters
- `key` Name of the metadata to be changed
- `value` New metadata value

----
## `item:uri()`
Get [URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier) of current item.

### Usage
```lua
local p_item = vlc.player.item()
print("Current item URI is: " .. p_item:uri())
```

### Return value
String containing the file URI

----
## `item:name()`
Get the display name of the item; does not include file extension.

### Usage
```lua
local p_item = vlc.player.item()
print("Current item name is: " .. p_item:name())
```

### Return value
String containing the file name

----
## `item:duration()`
Get item's duration in seconds or negative value if unavailable.

### Usage
```lua
local p_item = vlc.player.item()
print("Current item duration is: " .. p_item:duration())
```

### Return value
Number of seconds representing item's duration or value < 0 if duration is unavailable.

----
## `item:stats()`
Get statistics about an item.

### Usage
```lua
local p_item = vlc.player.item()
local stats = p_item:stats()
print("Current amount read: " .. tostring(stats.read_packets))
```

### Return value
Object representing statistics of an item; has the following fields:
.read_packets, .read_bytes, .input_bitrate, .demux_read_packets, .demux_read_bytes, .demux_bitrate, .demux_corrupted, .demux_discontinuity, .decoded_audio, .decoded_video, .displayed_pictures, .lost_pictures, .sent_packets, .sent_bytes, .send_bitrate, .played_abuffers, .lost_abuffers.

----
## `item:info()`
Get other item information (i.e. Stream(s) that make up the current item)

### Usage
```lua
local p_item = vlc.player.item()
```

### Return value
Table contianing item information; keys point to other tables.

----
# Rate and Position


----
## `get_rate()`
Get the playing rate.

### Usage
```lua
local rate = vlc.player.get_rate()
```

### Return value
Float representing the current playing rate; <1.0=slower, 1.0=Normal speed, >1.0=faster

----
## `set_rate()`
Set the playing rate.

### Usage
```lua
vlc.player.set_rate(0.8) -- slow it down
```

### Parameters
`rate` Float representing the new playing rate; <1.0=slower, 1.0=Normal speed, >1.0=faster

----
## `increment_rate()`
Increment the current rate by 1 step: New_Rate = Current_Rate * 1.1

### Usage
```lua
vlc.player.increment_rate()
```

----
## `decrement_rate()`
Decrement the current rate by 1 step: New_Rate = Current_Rate * 0.9

### Usage
```lua
vlc.player.decrement_rate()
```

----
## `get_position()`
Get the current position

### Usage
```lua
local pos = vlc.player.get_position()
```

### Return value
Float between 0 and 1 representing the position of the player as a proportion of item duration

----
## `get_time()`
Get the current player time.

### Usage
```lua
local time = vlc.player.get_time()
```

### Return value
Current player time, in [microseconds](https://en.wikipedia.org/wiki/Microsecond)

----
## `seek_by_pos_absolute()`
Seek (go to a position) by providing an absolute value.

### Usage
```lua
vlc.player.seek_by_pos_absolute(0.9) -- move position near the end
```

### Parameters
- `position` Float between 0 and 1 representing the new position of the player

----
## `seek_by_pos_relative()`
Seek (go to a position) by providing an relative value: New_Pos = Current_Pos + or - Relative_Value.

### Usage
```lua
vlc.player.seek_by_pos_relative(0.5)
```

### Parameters
- `adjust` Float representing the movement of the position of the player

----
## `seek_by_time_absolute()`
Seek (go to a position) by providing an absolute time.

### Usage
```lua
vlc.player.seek_by_time_absolute(1000000) -- seek to one second
```

### Parameters
- `position` Number representing the new player position measured in [microseconds](https://en.wikipedia.org/wiki/Microsecond)

----
## `seek_by_time_relative()`
Seek (go to a position) by providing an relative time value: New_Time = Current_Time + or - Relative_Value.

### Usage
```lua
vlc.player.seek_by_time_relative(1000000) -- adjust one second ahead
```

### Parameters
- `adjust` Number representing the movement of the position of the player measured in [microseconds](https://en.wikipedia.org/wiki/Microsecond)

----
# Titles and Chapters
Methods for changing the player based on title and chapter metadata.


## `get_title_index()`
Get the current title index.

### Return value
Integer: index of the current title

----
## `get_titles_count()`
Get the number of titles for the current media.

### Return value
Number >= 0 representing the number of titles for the current media

----
## `title_next()`
Tells the player to go to the next title.

----
## `title_prev()`
Tells the player to go to the previous title.

----
## `title_goto()`
Tells the player to go to a specific title.

### Parameters
- `index` Number >= 0 representing the index of the target title

----
## `get_chapter_index()`
Get the index of the current chapter.

### Return value
Integer: index of the current chapter

----
## `get_chapters_count()`
Get the number of chapters for the current title.

### Return value
Number >= 0 representing the number of chapters for the current media

----
## `chapter_next()`
Tells the player to go to the next chapter.

----
## `chapter_prev()`
Tells the player to go to the previous chapter.

----
## `chapter_goto()`
Tells the player to go to a specific chapter of the current title.

### Parameters
- `index` Number >= 0 representing the index of the target chapter

----
# Audio, Video and Stream Output


## `get_video_tracks()`
Get the list of video tracks.

### Return value
List of tack items, each item has the following fields: `.id`, `name`, `.selected` (boolean indicating whether the tack is selected)

----
## `toggle_video_track()`
Select/deselect a video track; turning it on or off.

### Parameters
- `id` Integer: Track id

----
## `next_video_frame()`
Advance the player one frame.

----
## `get_audio_tracks()`
Get the list of audio tracks.

### Return vale
List containing the audio tracks of the current media: uses the same format as [`get_video_tracks()`](#get_video_tracks).

----
## `toggle_audio_track()`
Select/deselect an audio track; turning it on or off.

### Parameters
- `id` Integer: Track id

----
## `get_audio_delay()`
Get audio delay for current media.

### Return value
Float: Delay for current audio track in seconds

----
## `set_audio_delay()`
Set audio delay for current media.

### Parameters
- `delay` New delay for current audio track in seconds

----
# Subtitles and SPU

## `add_subtitle()`
Attatch subtitle track to current media; load from file.

### Usage
```lua
vlc.player.add_subtitle("file://some/path/to/subtitle_file.srt", true) -- force selection
```

### Parameters
- `path` String contianing the path to the subtitle file or it's parent directory
- Optional
	- `autoselect` Boolean; if `true`, subtitle is tried by force, bypassing normal checks; value is `false` by default

----
## `add_subtitle_mrl()`
Attatch subtitle track to current media; load from [MRL](https://wiki.videolan.org/Media_resource_locator).

### Parameters
- `path` String contianing the MRL to the subtitle file or it's parent directory
- Optional
	- `autoselect` Boolean; if `true`, subtitle is tried by force, bypassing normal checks; value is `false` by default

----
## `get_subtitle_delay()`
Get subtitle delay for the current subtitle track.

### Return value
Float: Delay for current subtitle track in seconds

----
## `set_subtitle_delay()`
Set subtitle delay for current subtitle track.

### Parameters
- `delay` New delay for current subtitle track in seconds

----
## `get_spu_tracks()`
Get the list of [Sub-Picture Unit (SPU)](https://en.wikibooks.org/wiki/Inside_DVD-Video/Subpicture_Streams) tracks.

### Return vale
List containing the SPU tracks of the current media: uses the same format as [`get_video_tracks()`](#get_video_tracks).

----
## `toggle_spu_track()`
Select/deselect a SPU track; turning it on or off.

### Parameters
- `id` Integer track id

----
# Miscellaneous

## `is_playing()`
Determine whether input exists.

### Usage
```lua
if not (vlc.player.is_playing()) then
	print("Oh no: No media is playing!")
	return nil
end
local p_item = vlc.player.item()
```

### Return value
Boolean: `true` if input exists
