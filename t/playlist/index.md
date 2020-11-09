---
title: Playlist Parser Scripts
project: vlc-lua-docs
---
These scripts will be called to perform URL Translation or text playlist parsing.  
A large volume of info on these scripts can already be found [here](https://wiki.videolan.org/Documentation:Building_Lua_Playlist_Scripts) (some info here is taken from this resource).

# Playlist Parser VLC Fields

- `vlc.path` URL string (without the leading http:// or file:// element)
- `vlc.access` Access used ("http" for http://, "file" for file://, etc.)

----
# Playlist Paraser VLC Functions
These are methods in the global `vlc` object that are available to playlist parsers.

## `vlc.read()`
Read data from a playlist file.  
NOTE: Cannot be used in `probe()`.

### Parameters
- `numchars` Number of characters to read from the playlist file

### Return value
Characters read from the playlist file

----
## `vlc.readline()`
Like `vlc.read`, but only one line.  
NOTE: Cannot be used in `probe()`.

### Return value
Characters read from the playlist file line

----
## `vlc.peek()`
Like `vlc.read()`, but the first `numchars` characters are read from the playlist file.

### Parameters
- `numchars` Number of characters to read from the start of the playlist file

### Return value
Characters read from the playlist file

----
# Special Functions
These are functions that VLC expects in playlist parsers and are required in order for them to run properly.

## `probe()`
This function tells VLC if the Lua script should be used (function returns true) or not (function returns false) given a specific URL, read via `vlc.access`.

### Example
```lua
function probe()
  if vlc.access ~= "http"
  then
		return false
  end
  if string.match( vlc.path, "video.google.com/videoplay" )
  then
		return true
  else
		return false
  end
end
```

### Return value
This function should only return a boolean

----
## `parse()`
If the probe() function returns true, VLC will use the parse() to ask for the new playlist item(s) which need to be added.  
Data is passed to the parser from VLC via the `vlc.read()` and `vlc.readline()` functions and other VLC object fields.

### Example
```lua
function parse()
  item = {}
  item.path = "http://" .. string.gsub( vlc.path, "videoplay", "videogvp" )
  item.name = "Some Google video playlist"
  return { item }
end
```

### Return value
This function should return a table representing a new playlist item; these items should use the [same format as playlist.add()](../../m/playlist/#playlist-items).

----
# Examples
Here is a simple example of a playlist parser script authored by Pierre Ynard of the VideoLAN team, which handles [Vocaroo](https://vocaroo.com/) links.

```lua
-- Probe function.
function probe()
	return ( vlc.access == "http" or vlc.access == "https" )
		and string.match( vlc.path, "^vocaroo%.com/." )
end

-- Parse function.
function parse()
   -- The HTML page contains no metadata and is not worth parsing
   local id = string.match( vlc.path, "^vocaroo%.com/([^?]+)" )

   -- Dispatch media to correct CDN server
   local cdn = ( string.len( id ) == 10 or
					( string.len( id ) == 12 and string.match( id, "^1" ) ) )
			and "//media1.vocaroo.com/mp3/"
			or "//media.vocaroo.com/mp3/"

	local path = vlc.access..":"..cdn..id
	return { { path = path } }
end
```