---
title: Network Module
project: vlc-lua-docs
---
Network utilities, many of which are analogous to net utilities found in Linux.  
NOTE: File descriptors are passed to (and returned by) functions as non-negative integer values.

# Availability

| Script Types |
| ------------ |
| [Extension](../../t/extensions), [Interface](../../t/intf) |

----
# TCP Connections
Methods to create, manage and listen for TCP connections.

## `listen_tcp()`
Listen to TCP connections; creates [Net Listen Object](#listen-object).

### Usage
```lua
local l = vlc.net.listen_tcp("localhost", 1234)
while true do
	local fd = l:accept()
	if fd >= 0 do
		net.send(fd, "blabla")
		net.close(fd)
	end
end
```

### Parameters
- `host` Host to listen on
- `port` Port to listen on 

### Return value
A [listen object](#listen-object)

----
## `connect_tcp()`
Open a connection to the given host on a given port.

### Parameters
- `host` Host to connect to
- `port` Port to connect to

### Return value
File descriptor to accepted connection or `-1` on failure

----
## `send()`
Send data on an open TCP connection

### Usage
```lua
local conn = vlc.net.connect_tcp("some_host", 1234)
...
if should_send then
	vlc.net.send(conn, "data to send")
end
```

### Parameters
- `fd` File descriptor of open connection
- `buffer` String containing data to send
- Optional
	- `length` Length of data from `buffer` to send

### Return value
Integer value indicating the number of bytes sent on success; `-1` on failure

----
## `recv()`
Receive data from connection.

### Parameters
- `fd` File descriptor of open TCP connection
- Optional
	- `maxlength` Integer value specifying maximum number of bytes to read from connection

### Return value
String containing the data read from the TCP socket or `nil` if error occurred

----
## `close()`
Close an open connection.

### Parameters
- `fd` File descriptor of connection to be closed

----
# Other Methods
Some extra functions, most of which are non-network or deprecated.

## `poll()`
Polls file descriptor(s); similar to [poll](https://www.man7.org/linux/man-pages/man2/poll.2.html).  
Parameter is modified to include `revents` (returned events) which indicate what type of I/O is available for the file descriptor.  
All events refer to [poll event flags](#poll-event-flags).

### Parameters
- `fd-events` Table with `{ fd: events }` entries, where:
	- `fd` is a file descriptor to poll
	- `events` is a number that indicates the events you want to poll for (`POLLIN`, `POLLOUT`, `POLLPRI`)

### Return value
Integer value; positive or zero on success, negative on failure

----
## `read()`
Read data from a file.  
NOTE: Not available on Windows.

### Parameters
- `fd` Integer: File descriptor
- Optional
	- `maxlength` Integer specifying maximum length of data to be read; defaults to 1 byte

### Return value
String containing the read data or `nil`

----
## `write()`
Write data to a file.  
NOTE: Not available on Windows.

### Parameters
- `fd` File descriptor
- `buffer` String containing the data to be written
- Optional
	- `length` Number of bytes of `buffer` to be written; defaults to length of `buffer`

### Return value
Integer indicating the number of bytes written to `fd` or `-1` if write failed

----
## `url_parse()`
Alias for [strings.url_parse()](../strings/#url_parse).  
Deprecated since 3.0.0, kept for backwards compatibility.

----
## `stat()`
Similar to [stat()](https://en.wikipedia.org/wiki/Stat_(system_call)#stat()_functions) in POSIX C.

### Parameters
- `path` Valid path

### Return value
Table with the following fields:
- `.type` One of "file", "dir", "character device", "block device", "fifo", "symbolic link", "socket", "unknown"
- `.mode` Protection [mode](https://en.wikipedia.org/wiki/Unix_file_types#Representations)
- `.uid` User Identifier of owner
- `.gid` Group Identifier of owner
- `.size` Total file size, in bytes
- `.access_time` Time of last access
- `.modification_time` Time of last modification
- `.creation_time` Time of creation

----
## `opendir()`
List a directory's contents

### Parameters
- `path` String containing path to directory

### Return value
List of file and/or folder names

----
# Listen Object
The object returned by [listen_tcp()](#listen_tcp); houses the following methods.


## `listen:accept()`
Accept a TCP connection; similar to [accept](https://www.man7.org/linux/man-pages/man2/accept.2.html).  
This is a blocking call, for non-blocking use [listen:fds()](#listenfds).

### Return value
File descriptor for the accepted socket (non-negative integer)

----
## `listen:fds()`
Get file descriptors that can be polled before use.

### Return value
List of available socket file descriptors

----
# Poll Event Flags

- `POLLIN` There is data to read
- `POLLPRI` There is some exceptional condition on the file descriptor
- `POLLOUT` Writing is now possible
- `POLLERR` Error condition (only returned in revents)
- `POLLHUP` Hang up (only returned in revents)
- `POLLNVAL` Invalid request: fd not open (only returned in revents)
