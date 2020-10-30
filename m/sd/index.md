---
title: Services Discovery Module
project: vlc-lua-docs
---
Utilities for [Service Discovery](/vlc-lua-docs/t/sd) scripts.

# Availability

| Script Types |
| ------------ |
| [Services Discovery](../../sd) |

----
# Service Discovery Items
Items are the media elements provided by the service.


## `add_item()`
Adds an item to the root of the service panel.

### Usage
```lua
local song_path = vlc.strings.make_uri("/path/to/local/mp3/file.mp3")
local song_item = vlc.sd.add_item({path=song_path, title="Cool song", genre="The best genre"})
```

### Parameters
- `info` Table with the following keys:
	- `path` String containing URI/URL pointing to the item's media
	- Optional keys
		- Any [Metadata](#item-metadata) field
		- `duration` Number indicating the item's duration in seconds
		- `uiddata` String to build the input uid

### Return value
An [item object](#service-discovery-items)

----
## Item Setters
Each variable relating to an item's metadata settable via a function call. Each function's name conforms to the template `item:set_name(value)`, where "value" is a string containing the value to assign and "name" is the name of the [metadata](#item-metadata) to set.

### Example
```lua
local itm = vlc.sd.add_item({path=some_path, title="My Item"})
itm:set_language("French")
```

----
## Item Metadata
Items can have values assigned to the following metadata fields:
- `title`
- `artist`
- `genre`
- `copyright`
- `album`
- `tracknum`
- `description`
- `rating`
- `date`
- `setting`
- `url`
- `language`
- `nowplaying`
- `publisher`
- `encodedby`
- `arturl`
- `trackid`
- `tracktotal`
- `director`
- `season`
- `episode`
- `showname`
- `actors`

----
# Service Discovery Nodes
Nodes can be thought of as folder/directories/playlists. Each child of a node can be either an [item](#service-discovery-items) or another node.  
Each node has the following fields:
- `.title` The node's name
- `.arturl` URL to the node's playlist art

## `add_node()`
Add a node to the root of the service panel.

### Parameters
- `info` Table defining values for the node's fields: 
	- `title`
	- Optional keys
		- `arturl`

### Return value
A [node object](#service-discovery-nodes)

----
## `node:add_subitem()`
Add a child item to a node.

### Parameters
- `info` Table with the following keys:
	- `path` String containing URI/URL pointing to the item's media
	- Optional keys
		- Any [Metadata](#item-metadata) field
		- `duration` Number indicating the item's duration in seconds
		- `uiddata` String to build the input uid

### Return value
An [item object](#service-discovery-items)

----
## `node:add_subnode()`
Add a child node to a node.

### Parameters
- `info` Table defining values for the node's fields: 
	- `title`
	- Optional keys
		- `arturl`

### Return value
A [node object](#service-discovery-nodes)
