---
title: VLC Lua Docs
project: none
---
This is some documentation on the Lua scripting API for VLC Media Player. It covers the modules and script types that are available to VLC addon developers.

# Script Basics

### Installation
Scripts are placed into their own special folders in the VLC install directory. Below are the install directories for VLC scripts on different platforms.
- Windows (all users): %ProgramFiles%\VideoLAN\VLC\lua\
- Windows (current user): %APPDATA%\VLC\lua\
- Linux (all users): /usr/lib/vlc/lua/
- Linux (current user): ~/.local/share/vlc/lua/
- Mac OS X (all users): /Applications/VLC.app/Contents/MacOS/share/lua/
- Mac OS X (current user): /Users/%your_name%/Library/Application Support/org.videolan.vlc/lua/

## Types of Scripts

| Name | Description | Install Subdirectory | Version Range |
| ---- | ----------- | -------------------- | ------------- |
| [Art](./t/art) | Scripts called to download album/track artwork | /lua/meta/art/ | 0.9+ |
| [Extensions](./t/extensions) | Addons to VLC, found in the "Views" menu (has access to the [dialog](/vlc-lua-docs/m/dialog) module) | /lua/extensions/ | 1.1+ |
| [Interfaces](./t/intf) | Run in the background (custom interfaces must be enabled) | /lua/intf/ | 0.9+ |
| [Meta Fetcher](./t/fetcher) | ? | /lua/meta/fetcher | 1.1+ |
| [Meta Reader](./t/reader) | ? | /lua/meta/reader/ | 1.1+ |
| [Playlist Parsers](./t/playlist) | Scripts called to handle files when VLC is given a specific URL (e.g. when VLC gets http://somewebsite.com/playlist/id_string") | /lua/playlist/ | 0.9+ |
| [Services Discovery](./t/sd) | Used to generate media from a service (found on the sidebar) | /lua/sd/ | 1.1+ |

## Modules
In Lua, there are special tables called [Modules](https://www.lua.org/manual/5.1/manual.html#5.3). VLC's Lua Modules are available via the global `vlc` table and are assigned their own symbols (e.g. `vlc.config` => configuration module). Depending on the type of script that is running, certain modules may not be available.

| Name | Symbol(s) | Description | Availability |
| ---- | --------- | ----------- | ------------ |
| [Configuration](./m/config) | `config` | Access and modify VLC configuration options | Extension, Interface |
| [Dialog](./m/dialog) | `dialog` | Create and manage a dialog window (UI) | Extension |
| [Equalizer](./m/equalizer) | `equalizer` | Access and modify equalizer settings and presets | Interface |
| [Errno](./m/errno) | `errno` | Error values | Extension, Interface |
| [GetText](./m/gettext) | `gettext` | Alias for libvlc [gettext](https://en.wikipedia.org/wiki/Gettext) | Interface, Service Discovery |
| [HTTPd](./m/httpd)  | `httpd` | HTTP Daemon | Interface |
| [I/O](./m/io)  | `io` | Input/Output (i.e. file read/write, directories, etc...) | Extension, Interface |
| [Messages](./m/msg)  | `msg` | Output to the Messages console (Tools->Messages) | All types |
| [Miscellaneous](./m/misc)  | `misc` | Uncategroized functionality | Interface |
| [Network](./m/net)  | `net` | Some network methods | Extension, Interface |
| [Objects](./m/objects)  | `object` | Provides access to various objects | Extension, Interface, Meta, Service Discovery |
| [OSD](./m/osd)  | `osd` | On-screen display functionality (ex. Display OSD messages, modify channels) | Extension, Interface |
| [Player](./m/player) | `player` (pre 4.0: `input`) | Access the VLC player (Called "input" pre 4.0) | Extension, Interface, Service Discovery |
| [Playlist](./m/playlist)  | `playlist` | Access and modify playlists | Extension, Interface |
| [Random](./m/rand)  | `rand` | Get random numbers/bytes | Extension, Interface |
| [Renderer Discovery](./m/rd)  | `rd` | ? | ? |
| [Services Discovery](./m/sd)  | `sd` | Functionality for service discovery scripts (i.e. add nodes, items) | Service Discovery |
| [Stream](./m/stream)  | `stream`, `memory_stream`, `directory_stream` | Access to data streams and methods to read/modify them | All Types |
| [Strings](./m/strings)  | `strings` | String utils (ex. parse URI/URL, handle special chars) | All Types |
| [Variables](./m/var)  | `var` | Create and manipulate variables in VLC objects | All Types |
| [Video](./m/video)  | `video` | VLC video interface | Extension, Interface |
| [VLM](./m/vlm)  | `vlm` | VideoLAN Manager | Extension, Interface |
| [Volume](./m/volume)  | `volume` | Modify volume | Extension, Interface |
| [Windows](./m/win)  | `win` | Access to Windows console | Extension, Interface (Windows builds only) |
| [XML](./m/xml)  | `xml` | [XML](https://en.wikipedia.org/wiki/XML) reader, can be replaced by simplexml | All types |

### Non-VLC Modules
Outside of the modules in the global `vlc` table, VLC provides some other modules to aid in developing more complex scripts. These modules are found in VLC_INSTALL_PATH/lua/modules/ and must be explicitly imported into lua code using the built-in [require](https://www.lua.org/pil/8.1.html) function. Furthermore, any custom Lua modules placed in the lua/modules folder may also be 'required' in a Lua script.

```lua
require "module1" -- This works
local mod2 = require("module2") -- This also works
```

## LUAC
LUAC is a command line tool that lets you translate Lua scripts (.lua) into binary files (.luac), which are accepted as scripts by VLC when placed in an install directory.  
A more detailed description of LUAC can be found on it's [man page](https://www.lua.org/manual/5.1/luac.html), but here's a quick summary:

#### What LUAC does
- Precompiles Lua chunks into bytecode and saves them in a file, ensuring faster load times by saving on compilation time
- Adds resistance against small changes to a Lua program that might inadvertently change the program after it has been compiled

#### What LUAC does NOT do
- Create files that are necessarily smaller than the source code
- Speed up execution times or perform any optimizations that wouldn't already be done at runtime
- Apply any encryption or obfuscation that would prevent someone from easily reverse engineering Lua programs ([decompilers exist](http://luadec.luaforge.net/))
