---
title: Stream Module
project: vlc-lua-docs
---
VLC module for stream handling.

# Availability

| Script Types |
| ------------ |
| All Types |

----
# Stream Types
The stream module offers 3 types of streams, each accessed via the global `vlc` object with their own symbols: `vlc.stream`, `vlc.memory_stream` and `vlc.directory_stream`.


## `vlc.stream()`
Instantiate a stream object for a specific URL.

### Usage
```lua
local s = vlc.stream("http://www.videolan.org/")
```

### Parameters
- `url` String containing a URL to open

### Return value
A [Stream object](#stream-object)

----
## `vlc.memory_stream()`
Instantiate a stream object containing a specific string.

### Usage
```lua
local s = vlc.memory_stream("SGVsbG8sIHdvcmxkIQ==") -- "Hello, world!"
```

### Parameters
- `data` String containing some data

### Return value
A Memory [Stream object](#stream-object)

----
## `vlc.directory_stream()`
Instantiate a stream object for a specific local directory.

### Usage
```lua
local s = vlc.memory_stream("/home/guest/music")
```

### Parameters
- `path` String containing a path in the local directory

### Return value
A Directory [Stream object](#stream-object)

----
# Stream Object
Each type of stream has an instance method which returns a stream object with the following methods:


## `stream:read()`
Read data from the stream.

### Parameters
- `size` Integer value indicating the size of the read operation in bytes (should be > 0 and < size of stream)

### Return value
String containing the data that was read from the stream, otherwise `nil` on failure or if no data was read

----
## `stream:readline()`
Like [stream:read()](#streamread), but will only return the first line of any given file (i.e. until return/newline).

### Return value
String containing the first line from a stream, otherwise `nil` on read failure

----
## `stream:addfilter()`
Add a stream filter. With no parameters, this function tries to add all automatic stream filters.

### Parameters
- Optional
	- `filter` String containing the name of a filter to add

----
## `stream:readdir()`
Read file and folder listings from a stream.

### Parameters
- Optional
	- `filter` String containing a filter for file types to ignore (i.e. '.mp3')
	- `show_hidden` Boolean indicating whether to include hidden files while reading the directory

### Return value
List of file and folder input items corresponding to the stream directory

----
## `stream:getsize()`
Get stream size.

### Return value
Number value indicating the stream size in bytes.

----
## `stream:seek()`
Seek to a given position in the stream.

### Return value
Boolean value: `true` if seek succeeded, `false` otherwise