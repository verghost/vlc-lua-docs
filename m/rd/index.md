---
title: Renderer Discovery Module
project: vlc-lua-docs
---


# Renderer Discovery Object

## `create()`
Create a renderer discovery object.

### Usage
```lua
_rd = vlc.rd.create("mdns_renderer")
```

### Parameters
- `name` String containing the module type to use

### Return value
A new renderer discovery object

----
## `rd:list()`
List all known renderers.

### Return value
List of objects, each of which has the following fields:
- `type` The type of renderer
- `name` The name of the renderer
- `id` Renderer ID; to be provided to [rd:select()](#rdselect)
- `selected` Boolean value indicating whether the renderer is selected

----
## `rd:select()`
Select a renderer, or disable the current one.

### Parameters
- `id` Renderer identifier
