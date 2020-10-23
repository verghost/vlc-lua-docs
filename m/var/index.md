---
title: Variables Module
project: vlc-lua-docs
---
Create and manipulate variables in [VLC objects](/vlc-lua-docs/m/objects) ([Lua userdata](https://www.lua.org/pil/28.1.html) of the type "vlc_object").  


## `get()`
Get a specific value of a variable in a VLC object

### Usage
```lua
local vo = vlc.object.vout()
if vo then
	local autoscale = vlc.var.get(vo, "autoscale")
	if autoscale then
		vlc.msg.info("Auto-scale is on!")
	else
		vlc.msg.info("Auto-scale is off!")
	end
end 
```

### Parameters
- `object` VLC object
- `name` Name of variable in VLC object

### Return value
Value of `name` in `object` or `nil`

----
## `get_list()`
Get the value list (values the variable can be set to) and text list (dsiplay text for values) from a variable in a VLC object.

### Usage
```lua
local vo = vlc.object.vout()
if vo then
	local vals, texts = vlc.var.get_list(vo, "deinterlace-mode")
	vlc.msg.info(vals[11]) -- "ivtc"
	vlc.msg.info(texts[11]) -- "Film NTSC (IVTC)"
end 
```

### Parameters
- `object` VLC object
- `name` Name of variable in VLC object

### Return value
Returns two values:
1. Value list or error code (negative number)
2. Text list or error string

----
## `set()`
Set the value of a variable in a VLC object

### Parameters
- `object` VLC object
- `name` Name of variable in VLC object
- `value` Value to set to variable

### Return value
Two values that indicate how the set operation went:
- `code` 0 on success, VLC error code on failure
- `message` "no error" on success, otherwise an error string specifying the type of error

----
## `create()`
Create a variable in a VLC object.

### Parameters
- `object` VLC object
- `name` Name of new variable
- `value` Value to assing to the new variable

### Return value
Two values that indicate how the create operation went:
- `code` 0 on success, VLC error code on failure
- `message` "no error" on success, otherwise an error string specifying the type of error

Can also return `nil` in case of `nil` assignment

----
## `inherit()`
Determine the value inherited by a given vairable in a VLC object.

### Parameters
- `object` VLC object (If object is unset, the current module's object will be used)
- `name` Name of variable in VLC object

### Return value
Value inherited by the VLC object or `nil`

----
## `trigger_callback()`
Trigger the callbacks associated with a variable in a VLC object.

### Parameters
- `object` VLC object
- `name` Name of variable in VLC object

### Return value
Two values that indicate how the create operation went:
- `code` 0 on success, VLC error code on failure
- `message` "no error" on success, otherwise an error string specifying the type of error

----
## `libvlc_command()`
Issue a libvlc command.

### Parameters
- `name` Name of libvlc command
- `argument` Argument value for the command

### Return value
Two values that indicate how the create operation went:
- `code` 0 on success, VLC error code on failure
- `message` "no error" on success, otherwise an error string specifying the type of error

----
## `inc_integer()`
Increment a given integer variable in a VLC object.

### Parameters
- `object` VLC object
- `name` Name of integer variable in `object`

### Return value
New value of `name`

----
## `dec_integer()`
Decrement a given integer.

### Parameters
- `object` VLC object
- `name` Name of integer variable in `object`

### Return value
New value of `name`

----
## `count_choices()`
Get number of choices for a variable in a VLC object.

### Parameters
- `object` VLC object
- `name` Name of variable in `object`

### Return value
Number of choices for given variable

----
## `toggle_bool()`
Toggle a boolean variable in a VLC object.

### Parameters
- `object` VLC object
- `name` Name of boolean variable in `object`

### Return value
New value of `name`
