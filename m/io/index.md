---
title: IO Module
project: vlc-lua-docs
---
Input/Output to/from local file system.  
Error codes returned from methods in this module will correspond to the [ErrNo](../errno) module.

# Availability

| Script Types |
| ------------ |
| [Extension](../../t/extensions), [Interface](../../t/intf) |

----
## `open()`
Open a file; similar to Lua's [io.open](https://www.lua.org/manual/5.1/manual.html#pdf-io.open) method.

### Usage
```lua
local f = open("hello.txt", 'rt') -- only read text
```

### Parameters
- `path` String containing the path to a file
- Optional
	- `mode` String specifying which [mode](#file-modes) in which to open the file; defaults to 'r'

### Return value
A [File Object](#file-object)

----
## `mkdir()`
Similar to [mkdir(2)](https://linux.die.net/man/2/mkdir); creates a directory.

### Usage
```lua
local c1, c2 = vlc.io.mkdir("/this/path/might/exist/folder_name")
if c1 == -1 then -- operation failed
	if c2 == vlc.errno.EACCES then
		print("Oh no: No permission")
	else
		print("Some error occurred!")
else
	print("All's good!")
end
```

### Parameters
- `path` Path to new directory
- `mode` String: Mode of operation (can be octal representation)

### Return value
Two integer values:
- First Value = 0 on success, non 0 value in case of failure  
- Second Value = 0 On success, [error code](../errno) in case of failure

----
## `readdir()`
List all files and folders in a given directory.

### Usage
```lua
local files_in_dir = vlc.io.readdir("/path/to/existing/directory/")
for i,f in pairs(files_in_dir) do
	vlc.msg.info("File #" .. i .. " in directory is: " .. f)
end
```

### Parameters
- `path` String: Path to existing directory

### Return value
List of file/folder names (empty if directory is empty)

----
## `unlink()`
Similar to [os.remove](https://www.lua.org/manual/5.1/manual.html#pdf-os.remove); unlinks/removes a file.

### Parameters
- `path` Path to the file

### Return value
Two integer values:
- First Value = 0 on success, non 0 value in case of failure  
- Second Value = 0 On success, [error code](../errno) in case of failure

----
# File Modes
To open a file, a 'mode' must be specified. This is done via strings where the modes and modifiers are each represented by a character.

Base Modes:
- 'r' Read Only
- 'w' Write Only (will overwrite existing file)
- 'a' Append mode (will add data to an existing file when writing)
- '+' Read and Write

Modifiers can also be added to modes to change the way they work
- 'x' Exclusive open; forces method failure if file exists 
- 't' Text Mode; only text will be read from the file (overrides 'b')
- 'b' Binary mode (overrides 't')

As an example, `f = open("hello.exe", 'rt')` would open, but `f:read("*a")` would not return all data from the file.

----
# File Object
Represents an open file.


## `file:read()`
Read from open file.  
Throws an error if called on closed file.

### Usage
```lua
local f = open("some_file_to_read.txt", 'rt')
local text = f:read("*a")
vlc.msg.info("There are " .. string.len(text) .. " characters in the file!")
```

### Parameters
- Optional
	- `mode` One of the following:
		- An integer, indicating how many characters (bytes) should be read from the file
		- A read mode string; one of:
			- "*l" Read a line from the current position in the file
			- "*n" Read a number from the file
			- "*a" Read all data from the file (limited by the value of C++ `SIZE_MAX` constant)
	
	Default value is "*l"

### Return value
Either `nil` or a string containing the data that was read

----
## `file:write()`
Write data to a file.  
Throws an error if called on closed file or a file opened without write permissions.

### Usage
```lua
local f = open("some_file.txt", 'a')
f:write("Hello, world!") -- append "Hello, world!"
```

### Parameters
- `data` Data to write to the file; can be either a Number or a String,
- Optional
	- `...` Additional arguments specifying more data to write

### Return value
Boolean value: `true` if write operation succeeded, else `false`

----
## `file:seek()`
Set the internal position of the file, where file data is read from and written to.  
Throws an error if called on closed file.

### Usage
```lua
local f = open("user_string_length.txt", 'r')
f:seek("set", 41)
vlc.msg.info("42nd character is: " .. f:read(1))
```

### Parameters
- `mode` String containing the seek mode; one of:
	- "set" Offset will reference the beginning of the file
	- "end" Seek to end of file
- Optional
	- `offset` Number of bytes to seek to (used in "set" mode); defaults to 0

### Return value
Number specifying the new internal position

----
## `file:flush()`
Flushes output buffer (calls [fflush](https://www.cplusplus.com/reference/cstdio/fflush/) internally).

----
## `file:close()`
Closes an open file.
