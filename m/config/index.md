---
project: vld
vld-meta-version: 9.0,1.0:2.0,9.0,+
---

# Configuration Module

<h6 class="vld-version">Version: &#62;9.0</h6>

Access and modify configuration options.  
Option names can be found in the `vlcrc` file in the folder given by `vlc.config.configdir()` (usually %appdata%\vlc\ on windows).

----
# get()
Get the value of a VLC configuration option.
### Syntax
```lua
local option = vlc.config.get(name)
```
### Parameters
- `name` String representing the name of the vlc config option

### Return value
The value of the setting corresponding to `name`. If `name` does not correspond to an existing option, then get() fails.

----
# set()
Se the value of a VLC configuration option.
### Syntax
```lua
vlc.config.set(name, value)
```
### Parameters
- `name` Name of the vlc config option
- `value` Value to assign to the config option

### Return value
None

----
# datadir()
Get the VLC data directory.
### Syntax
```lua
local dataDir = vlc.config.datadir()
```
### Parameters
None

### Return value
A string representing the path to the data directory.

----
# datadir_list()
Get the list of possible data directories in order of priority, each will have `str` appended onto the end.
### Syntax
```lua
local dirList = vlc.config.datadir_list(str)
```
### Parameters
`str` A string that will be appended onto the end of each returned path.

### Return value
An indexed table of strings, each representing a data directory path.

----
# userdatadir()
Get the current user's VLC data directory.
### Syntax
```lua
local udataDir = vlc.config.userdatadir()
```
### Parameters
None

### Return value
A string representing the path to the current user's VLC data directory.

----
# homedir()
Get the current user's home directory.
### Syntax
```lua
local homeDir = vlc.config.homedir()
```
### Parameters
None

### Return value
A string representing the path to the current user's home directory.

----
# configdir()
Get the current user's VLC config directory.
### Syntax
```lua
local configDir = vlc.config.configdir()
```
### Parameters
None

### Return value
A string representing the path to the current user's VLC config directory.

----
# cachedir()
Get the current user's VLC cache directory.
### Syntax
```lua
local cacheDir = vlc.config.cachedir()
```
### Parameters
None

### Return value
A string representing the path to the current user's VLC cache directory.
