---
title: HTTPd Module
project: vlc-lua-docs
---

An [HTTP daemon](https://www.webopedia.com/TERM/H/HTTPD.html) for use in Lua interfaces; connects to VLC's internal [HTTP](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol) server API.

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
The functionality from this module is leveraged via the methods provided by an instance of this object.

----
## `httpd:handler()`
Adds a handler for a given url. Can serve responses for GET, POST and HEAD requests, with different content types.

### Usage
```lua
-- Run with --http-host 127.0.0.1 --http-port 4441 (for example)
-- The following handler will serve requests at http://127.0.0.1/test
local hd = vlc.httpd()
local handler = hd:handler("/test", nil, "password", handler_callback, nil)
```

### Parameters
- `url` String containing the [URL](https://en.wikipedia.org/wiki/URL) to be served on request
- `user` String containing a username to be used to authenticate connecting clients (Must be `nil` or string)
- `password` String containing a password to be used to authenticate connecting clients (Must be `nil` or string)
- `callback` Reference to a [handler callback](#handler-callback) function; this will be called to handle connections
- `data` Data to be sent to the callback (can be `nil`)

### Return value
[Userdata](https://stackoverflow.com/a/4332717) for the newly created handler

----
## `httpd:file()`
Serve a file at a given url, with a given type. Allows for a broader content type response; does not support passing POST data.

### Usage
```lua
-- Run with --http-host 127.0.0.1 --http-port 4441 (for example)
-- The following handler will serve HTML data at http://127.0.0.1/test
local hd = vlc.httpd()
hd:file("/test", "text/html", nil, "password", file_callback, nil)
```

### Parameters
- `url` [URL](https://en.wikipedia.org/wiki/URL) to be served on request
- `mime` The [MIME type](https://en.wikipedia.org/wiki/Media_type) of the file
- `user` A username to be used to authenticate connecting clients (Must be `nil` or string)
- `password` A password to be used to authenticate connecting clients (Must be `nil` or string)
- `callback` Reference to a [file callback](#file-callback) function; this will be called to handle connections
- `data` Data to be sent to the callback (can be `nil`)

### Return value
[Userdata](https://stackoverflow.com/a/4332717) for the newly created file service

----
## `httpd:redirect()`
Redirect all connections from one URL to another

### Usage
```lua
-- Run with --http-host 127.0.0.1 --http-port 4441 (for example)
-- The following will redirect http://127.0.0.1 to http://127.0.0.1/hello
local hd = vlc.httpd()
hd:redirect("/hello", "/")
```

### Parameters
- `url_dst` String containing the destination URL
- `url_src` String containing the (source) URL to redirect

### Return value
[Userdata](https://stackoverflow.com/a/4332717) for the newly created redirect

----
# HTTPd Callbacks
These are functions that are passed to HTTPd methods and later called by VLC when a request is made. The functions should be defined in the global scope and passed to the constructor that requires them.

----
## Handler Callback
Callback for the [HTTPd Handler](#httpdhandler).

### Example
```lua
function handler_callback(data, url, query, r_type, r_in, addr, host)
  local callback = function()
    if r_type == 2 then -- HTTP GET request
      print("We have a GET request at: " .. url)
      if not (query == nil) then
        print("The following query string was sent: " .. query)
      end
    end
    return "Status: 200\nContent-Type: text/plain\nContent-Length: 13\n\nHello, World!\n"
  end
  
  -- pcall can be helpful for error detection; especially since lua errors can kill httpd
  local ok, content = pcall(callback) 
  if not ok then
      return "Status: 404\nContent-Type: text/plain\nContent-Length: 5\n\nError\n"
  end
  return content
end
```

### Parameters
- `data` Data passed from the constructor
- `url` URL that was requested (e.g. "/" when requesting the root page)
- `query` [Query string](https://en.wikipedia.org/wiki/Query_string) (If sent, otherwise nil)
- `type` Type of HTTP request; values are usually: 2=GET, 3=HEAD, 4=POST
- `in` Input received (POST data), otherwise empty string ("")
- `addr` Remote client IP address
- `host` `nil`
<!-- 
TODO: Look into this: Is host param an unused value?
Source code sends NULL as host value from httpd_HandlerCallBack -> vlclua_httpd_handler_callback
https://code.videolan.org/videolan/vlc/-/blob/master/src/network/httpd.c#L435
-->

### Return value
A string containing the reply to be issued to the remote client

----
## File Callback
Callback for the [HTTPd file](#httpdfile) method.

### Example
```lua
function file_callback(data, query)
  if not (query == nil) then print("Query string: " .. query) end
  local c_data = tostring(data)
  if c_data == "nil" then
    c_data = ""
  end
  return [[<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Hello, world!</title>
    <meta charset="utf-8">
  </head>
  <body>
    <h1>Hello, world!</h1>
    <h2>Data from constructor:</h2>
    <p>]] .. c_data .. [[</p>
  </body>
</html>
]]
end
```

### Parameters
- `data` Data passed from the constructor
- `query` [Query string](https://en.wikipedia.org/wiki/Query_string) (If sent, otherwise nil)

### Return value
A string containing the reply to be issued to the remote client
