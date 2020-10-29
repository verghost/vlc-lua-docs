---
title: XML Module
project: vlc-lua-docs
---
Handle [XML](https://en.wikipedia.org/wiki/XML) documents.  
NOTE: The simplexml module can also be used to parse XML documents.


## `xml()`
Get an XML object, which provides XML reader.

### Return value
XML Object

----
# XML Reader
Provided by the XML Object, used to read and parse XML data.


## `xml:create_reader()`
Create an XML reader for a given stream.

### Parameters
- `stream` [Stream object](../stream/#stream-object)

### Return value
XML Reader object

----
## `reader:next_node()`
Get information about the next node in the XML document.

### Return value
Returns two values:
- `type` Integer; 0 on none or error, 1 on start of XML element, 2 on end of XML element, 3 on text
- `name` Name of XML node (not returned when `type` <= 0)

----
## `reader:next_attr()`
Get information about the next attribute in an XML document.

### Return value
Returns two values on success `nil` otherwise:
- `name` String containing the name of the attribute
- `value` String containing the value of the attribute

----
## `reader:node_empty()`
Determine whether the previous invocation of [reader:next_node()](#readernext_node) refers to an empty node.

### Return value
Integer value: -2 on failure, 1 on empty node, 0 on non-empty node
