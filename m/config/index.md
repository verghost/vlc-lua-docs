---
title: Configuration Module
project: vlc-lua-docs
---
Access and modify configuration options.  
Option names can be found in the `vlcrc` file in the folder given by `vlc.config.configdir()` (usually %appdata%\vlc\ on windows).

# Availability

| Script Types |
| ------------ |
| [Extension](../../t/extensions), [Interface](../../t/intf) |

----
## `get()`
Get the value of a VLC configuration option.

### Usage
```lua
local option = vlc.config.get(name)
```
### Parameters
- `name` String representing the name of the vlc config option

### Return value
The value of the setting corresponding to `name`. If `name` does not correspond to an existing option, then get() fails.

----
## `set()`
Se the value of a VLC configuration option.

### Usage
```lua
vlc.config.set(name, value)
```

### Parameters
- `name` Name of the vlc config option (set fails if name is invalid)
- `value` Value to assign to the config option

----
## `datadir()`
Get the VLC data directory.

### Usage
```lua
local dataDir = vlc.config.datadir()
```

### Return value
A string representing the path to the data directory.

----
## `datadir_list()`
Get the list of possible data directories in order of priority, each will have `str` appended onto the end.

### Usage
```lua
local dirList = vlc.config.datadir_list(str)
```

### Parameters
`str` A string that will be appended onto the end of each returned path.

### Return value
An indexed table of strings, each representing a data directory path.

----
## `userdatadir()`
Get the current user's VLC data directory.

### Usage
```lua
local udataDir = vlc.config.userdatadir()
```

### Parameters
None

### Return value
A string representing the path to the current user's VLC data directory.

----
## `homedir()`
Get the current user's home directory.

### Usage
```lua
local homeDir = vlc.config.homedir()
```

### Return value
A string representing the path to the current user's home directory.

----
## `configdir()`
Get the current user's VLC config directory.

### Usage
```lua
local configDir = vlc.config.configdir()
```

### Return value
A string representing the path to the current user's VLC config directory.

----
## `cachedir()`
Get the current user's VLC cache directory.

### Usage
```lua
local cacheDir = vlc.config.cachedir()
```

### Return value
A string representing the path to the current user's VLC cache directory.
