---
title: HTTPd Module
---

An [HTTP daemon](https://www.webopedia.com/TERM/H/HTTPD.html) for use in Lua interfaces. Connects to VLC's internal [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)/[RTSP](https://en.wikipedia.org/wiki/Real_Time_Streaming_Protocol) server API.

----
## `httpd()`
Constructor for the HTTP daemon object. 

### Usage
```lua
local hd = vlc.httpd()
```

### Return value
An httpd object representing the newly created HTTP daemon

----
# HTTPd Object
The main functionality from the module is leveraged via the methods provided by an instance of this object.

----
## `httpd:handler()`
Adds a handler for a given url.

### Usage
```lua
-- VLC launched with .\vlc.exe --http-host 127.0.0.1 --http-port 4441
function callback_hd(data, url, request, type, in, addr, host)
  ...
end

local hd = vlc.httpd()
local handler = hd:handler(url, nil, "password", callback_hd, nil)
```

### Parameters
- `url` String containing the [URL](https://en.wikipedia.org/wiki/URL)
- `user` String representing a username to be used to authenticate connecting clients (Must be `nil` or string)
- `password` String representing a password to be used to authenticate connecting clients (Must be `nil` or string)
- `callback` Reference to a [handler callback](#handler-callback) function; this will be called to handle connections
- `data` Data to be sent to the callback (can be `nil`)

### Return value
Userdata representing the newly created handler

----
## `httpd:file()`
Add a file for given url with a given mime type.

----
## `httpd:redirect()`
Redirect all connections from one URL to another

### Usage
```lua
local hd = vlc.httpd()
```

### Parameters
- `url_dst` String contianing the destination URL
- `url_src` String contianing the (source) URL to redirect


----
# HTTPd Callbacks
These are functions that are called by VLC once an operation is complete or when some event has occured. The functions should be defined in the global scope and passed to the constructor that requires them.

----
## Handler Callback
This is the callback for the [HTTPd Handler](#httpdhandler)

### Parameters
- `data` Data pased from the handler constructor
- `url` URL that was requested (e.g. "/" when requesting the root page)
- `request`
- `type` Type of HTTP request; values are usually: 2=GET, 3=HEAD, 4=POST
- `in` Input recieved (POST data)
- `addr` Address requested (ip)
- `host`

### Return value
A string containing the reply

----
## File Callback
Callback for the [HTTPd file](#httpfile) method.

### Parameters
- `data`
- `request`

### Return value
A string containing the reply
