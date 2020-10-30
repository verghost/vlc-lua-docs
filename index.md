---
title: VLC Lua Docs
---

### **A Few Thing To Note**
- The information in these docs is based on VLC 4.0.0, so these docs may differ significantly from earlier versions of the Lua API.
- This is NOT a Lua tutorial. There are plenty of [good ones](http://lua-users.org/wiki/TutorialDirectory) out there, though.
- The version of these docs on verghost.com might not be the most recent version. Changes are made to [this repo](https://github.com/verghost/vlc-lua-docs/) and are pulled as a subtree.

# Script Basics

### What are VLC Lua Scripts?
Scripts are small one-file programs written in [Lua](https://en.wikipedia.org/wiki/Lua_(programming_language)). These programs are run by VLC and can access internal VLC data and functionality via the VLC Lua API, which these docs attempt to describe.

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
| [Art](https://verghost.com/vlc-lua-docs/t/art) | Scripts called to download album/track artwork | /lua/meta/art/ | 0.9+ |
| [Extensions](https://verghost.com/vlc-lua-docs/t/extensions) | Addons to VLC, found in the "Views" menu (has access to the [dialog](/vlc-lua-docs/m/dialog) module) | /lua/extensions/ | 1.1+ |
| [Interfaces](https://verghost.com/vlc-lua-docs/t/intf) | Run in the background (custom interfaces must be enabled) | /lua/intf/ | 0.9+ |
| [Meta Fetcher](https://verghost.com/vlc-lua-docs/t/fetcher) | ? | /lua/meta/fetcher | 1.1+ |
| [Meta Reader](https://verghost.com/vlc-lua-docs/t/reader) | ? | /lua/meta/reader/ | 1.1+ |
| [Playlist Parsers](https://verghost.com/vlc-lua-docs/t/playlist) | Scripts called to handle files when VLC is given a specific URL (e.g. when VLC gets http://somewebsite.com/playlist/id_string") | /lua/playlist/ | 0.9+ |
| [Services Discovery](https://verghost.com/vlc-lua-docs/t/sd) | Used to generate media from a service (found on the sidebar) | /lua/sd/ | 1.1+ |

### Special Functions
While a custom script is running, VLC will provide (and try to execute) a number of different functions. How they are defined and implemented determines the look and functionality of a script, or whether the script runs at all. Different script types expect different identifiers to be defined, so see the type pages for more detail.

## Modules
In Lua, there are special tables called [Modules](https://www.lua.org/manual/5.1/manual.html#5.3). VLC's Lua Modules are available via the global `vlc` table and are assigned their own symbols (e.g. `vlc.config` => configuration module). Depending on the type of script that is running, certain modules may not be available.

| Name | Symbol(s) | Description | Availability |
| ---- | --------- | ----------- | ------------ |
| [Configuration](https://verghost.com/vlc-lua-docs/m/config) | `config` | Access and modify VLC configuration options | Extension, Interface |
| [Dialog](https://verghost.com/vlc-lua-docs/m/dialog) | `dialog` | Interface to the DialogUI object | Extension |
| [Equalizer](https://verghost.com/vlc-lua-docs/m/equalizer) | `equalizer` | Access and modify equalizer settings and presets | Interface |
| [Errno](https://verghost.com/vlc-lua-docs/m/errno) | `errno` | Error values | Extension, Interface |
| [GetText](https://verghost.com/vlc-lua-docs/m/gettext) | `gettext` | Alias for libvlc [gettext](https://en.wikipedia.org/wiki/Gettext) | Interface, Service Discovery |
| [HTTPd](https://verghost.com/vlc-lua-docs/m/httpd)  | `httpd` | Interface to the VLC HTTP Daemon constructor | Interface |
| [I/O](https://verghost.com/vlc-lua-docs/m/io)  | `io` | Input/Output (i.e. file read/write, directories, etc...) | Extension, Interface |
| [Messages](https://verghost.com/vlc-lua-docs/m/msg)  | `msg` | Output to the Messages console (Tools->Messages) | All types |
| [Miscellaneous](https://verghost.com/vlc-lua-docs/m/misc)  | `misc` | Uncategroized functionality | Interface |
| [Network](https://verghost.com/vlc-lua-docs/m/net)  | `net` | Various network methods | Extension, Interface |
| [Objects](https://verghost.com/vlc-lua-docs/m/objects)  | `object` | Provides access to various objects | Extension, Interface, Meta, Service Discovery |
| [OSD](https://verghost.com/vlc-lua-docs/m/osd)  | `osd` | On-screen display functionality (ex. Display OSD messages, modify channels) | Extension, Interface |
| [Player](https://verghost.com/vlc-lua-docs/m/player) | `player` (pre 4.0: `input`) | Access the VLC player interface (Called "input" pre 4.0) | Extension, Interface, Service Discovery |
| [Playlist](https://verghost.com/vlc-lua-docs/m/playlist)  | `playlist` | Access and modify playlists | Extension, Interface |
| [Random](https://verghost.com/vlc-lua-docs/m/rand)  | `rand` | Get random numbers/bytes | Extension, Interface |
| [Renderer Discovery](https://verghost.com/vlc-lua-docs/m/rd)  | `rd` | ? | ? |
| [Services Discovery](https://verghost.com/vlc-lua-docs/m/sd)  | `sd` | Functions for service discovery scripts (i.e. add nodes, items) | Service Discovery |
| [Stream](https://verghost.com/vlc-lua-docs/m/stream)  | `stream`, `memory_stream`, `directory_stream` | Access to data streams and methods to read/modify them | All Types |
| [Strings](https://verghost.com/vlc-lua-docs/m/strings)  | `strings` | String utils (ex. parse URI/URL, handle special chars) | All Types |
| [Variables](https://verghost.com/vlc-lua-docs/m/var)  | `var` | Interface to VLC internal variables(?) | All Types |
| [Video](https://verghost.com/vlc-lua-docs/m/video)  | `video` | Change video interface | Extension, Interface |
| [VLM](https://verghost.com/vlc-lua-docs/m/vlm)  | `vlm` | VideoLAN Manager object instance method | Extension, Interface |
| [Volume](https://verghost.com/vlc-lua-docs/m/volume)  | `volume` | Modify volume | Extension, Interface |
| [Windows](https://verghost.com/vlc-lua-docs/m/win)  | `win` | Access to Windows console | Extension, Interface (Windows builds only) |
| [XML](https://verghost.com/vlc-lua-docs/m/xml)  | `xml` | [XML](https://en.wikipedia.org/wiki/XML) reader, can be replaced by simplexml | All types |

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
