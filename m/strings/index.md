---
title: Strings Module
project: vlc-lua-docs
---
String utilities.


## `decode_uri()`
Decode one or more [URIs](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier).

### Usage
```lua
local u1, u2 = vlc.strings.decode_uri("URI_VALUE", "URI_VALUE")
```

### Parameters
- `...` String values containing URIs to decode

### Return value
String value(s) containing the decoded URI(s) passed to the function (as many values as were passed)

----
## `encode_uri_component()`
Encode one or more URIs.

### Parameters
- `...` String values containing URIs to be encoded

### Return value
String value(s) containing the encoded URI(s) passed to the function (as many values as were passed)

----
## `make_uri()`
Convert a file path to a URI.

### Parameters
- `path` String containing the path to be converted

### Return value
String value: URI corresponding to a given path; may also return `path` (file path) if `path` does not contain "://"

----
## `make_path()`
Convert a URI to a file path.

### Parameters
- `path` String containing the URI to be converted to a path

### Return value
String value: Path corresponding to a given URI

----
## `url_parse()`
Parse a [URL](https://en.wikipedia.org/wiki/URL) into a table.

### Parameters
- `path` String containing the URI to be parsed

### Return value
A table containing the following fields:
- `protocol` URL protocol
- `username` URL username (in userinfo)
- `password` URL password (in userinfo)
- `host` URL host
- `port` URL port number
- `path` URL path
- `option` URL options

NOTE: Fields and values are only included in the resulting table if they exist in the given URL.

----
## `resolve_xml_special_chars()`
Resolve XML special characters in one or more strings.

### Parameters
- `...` String value(s) containing XML characters

### Return value
Resolved string value(s) (as many values as were passed)

----
## `convert_xml_special_chars()`
Escape XML special characters in one or more strings.

### Parameters
- `...` String value(s) to be converted

### Return value
Converted string value(s) (as many values as were passed)

----
## `from_charset()`
Convert a string from a specified character encoding into UTF-8.

### Parameters
- `str` String to be converted

### Return value
UTF-8 encoded string
