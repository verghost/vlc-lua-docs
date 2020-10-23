---
title: VLM Module
project: vlc-lua-docs
---
The Lua [VideoLAN Manager](https://www.videolan.org/developers/vlc/doc/doxygen/html/group__server.html) wrapper.


# The VLM Object
Object that provides access to VLM methods.  
NOTE: If the VLM object is deleted and one last reference remains to it in the script, all VLM items will be deleted.

## `vlm()`
Instanciate a VLM object.

### Return value
VLM object instance

----
## `vlm:execute_command()`
Execute a VLM command by passing it to the VLM shell.

### Usage
```lua
local v = vlc.vlm()
local msg = v:execute_command("show media") -- displays a summary of media states
if msg.children and #msg.children > 0 then
	for i,c in pairs(msg.children) do
		vlc.msg.info("Media State #" .. i .. ": " .. c)
	end
end

```

### Parameters
- `cmd` String containing the command to be executed (must follow [VLM command line syntax](https://wiki.videolan.org/Documentation:Streaming_HowTo/VLM/#Command_line_syntax))

### Return value
Returns a message table with the following fields:

- `"name"` String containing the name of the message/command
- `"value"` String value of the message (not included in message table
- `"children"` List of children, where each child is it's own message table

NOTE: `"value"` and `"children"` fields are included only if they are available.
