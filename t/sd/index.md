---
title: Services Discovery Scripts
project: vlc-lua-docs
---
Services discovery scripts (SDs) are scripts that, as the name might suggest, discover media files from online services. Defining an SD will cause it to appear as an option in the side panel of VLC under the subheading "Internet".  
Once the media has been discovered and handled, they can be presented to the user can add media items to the SD panel, which can then be played by the user.  
Managing these items is done with the [SD Lua module](../../m/sd/).

----
# Special Functions
When extension scripts are started VLC looks for a few functions, some of which are necessary for the script to continue execution.  
These functions might be required to accept parameters and/or return specific values.

## `descriptor()`
This is one of the most important special functions, expected in most VLC Lua scripts. Defining this function is a requirement for the SD to be registered by VLC.  

### Return value
This function only needs to return a table of information, which can have the following fields:

- `title` This is the title of the SD (the only mandatory field)
- `capabilities` A list containing one or more of the following strings, each of which will tell VLC what functionality to enable (or disable) for the SD
	- "search": Indicates that the SD handles searches (causes VLC to call the search() function)

----
## `main()`
This function is called when the SD is started.

----
## `search()`
Called by VLC when the user searches the SD panel.  
Only called when the "search" capability is returned from descriptor().

### Parameters
- `query_string` String containng the search query

----
# Lazy Initialization
Due to the way that SDs are implemented, you cannot make a global/top-level require for a VLC Lua module (including those in the lua/modules directory.  
Instead, it is recommended that SD developers "lazily load" them from the main() and/or search() functions.
```lua
lazily_loaded = false
dkjson        = nil

function lazy_load()
  if lazily_loaded then return nil end
  dkjson = require("dkjson")
  lazily_loaded = true
end

function descriptor()
  return { title = "..." }
end

function main()
  lazy_load()
  -- Do stuff here
end

function search(query)
  lazy_load()
  -- Do stuff here
end
```