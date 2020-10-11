# VLC Lua Docs
The aim of these docs is to (hopefully) help aspiring developers. All info in these docs has been compiled from a number of disparate readme files, [VideoLAN Forum](https://forum.videolan.org/) posts, [the Wiki](https://wiki.videolan.org/), [code from existing VLC addons](https://addons.videolan.org) and of course my own tinkering and staring at the source code.

### **A Few Thing To Note**
- This is NOT a Lua tutorial. There are plenty of good ones out there, though.
- This documentation intentionally overlooks VLC [skins](https://www.videolan.org/vlc/skins.html). This is mainly because they already have their own [skin editor application](https://www.videolan.org/vlc/skins.html) and are a little outdated (last release was 25-Aug-2009). Plus they require a totally different "skinnable" U.I. which looks real ugly.
- The VLC app has undergone lots of changes, so Lua modules have come, gone and been moved since version. In these docs, I refer to the [latest release](https://get.videolan.org/vlc/last/) as of October 2020.
- Finally, for the sake of streamlining terminology, I'm going to use "addon", "plugin", "extension", etc as categories of "scripts".

## Script Basics
There are a few types of lua scripts each with their own page instead of laying everything out here. I will use this page to cover the basics.

### What are VLC Lua Scripts?
Scripts are small one-file programs written in [Lua](https://en.wikipedia.org/wiki/Lua_(programming_language)). These programs are run by VLC and can access internal VLC data and functionality via the VLC Lua API, which these docs attempt to describe.

### Installation
Scripts are placed into their own special folders in the VLC install directory. Below are the default install directories for VLC on different platforms.
- Windows (all users): %ProgramFiles%\VideoLAN\VLC\lua\
- Windows (current user): %APPDATA%\VLC\lua\
- Linux (all users): /usr/lib/vlc/lua/
- Linux (current user): ~/.local/share/vlc/lua/
- Mac OS X (all users): /Applications/VLC.app/Contents/MacOS/share/lua/
- Mac OS X (current user): /Users/%your_name%/Library/Application Support/org.videolan.vlc/lua/

### Types of Scripts

| Name | Description | Install Subdirectory | Version Range |
| ---- | ----------- | -------------------- | ------------- |
| [Art](https://verghost.com/vlc-lua-docs/t/art) | ? | /lua/meta/art/ | 0.9+ |
| [Extensions](https://verghost.com/vlc-lua-docs/t/extensions) | ? | /lua/extensions/ | 1.1+ |
| [Interfaces](https://verghost.com/vlc-lua-docs/t/intf) | ? | /lua/intf/ | 0.9+ |
| [Meta Fetcher](https://verghost.com/vlc-lua-docs/t/fetcher) | ? | /lua/meta/fetcher | 1.1+ |
| [Meta Reader](https://verghost.com/vlc-lua-docs/t/reader) | ? | /lua/meta/reader/ | 1.1+ |
| [Playlist Parsers](https://verghost.com/vlc-lua-docs/t/playlist) | ? | /lua/playlist/ | 0.9+ |
| [Services Discovery](https://verghost.com/vlc-lua-docs/t/sd) | ? | /lua/sd/ | 1.1+ |

### Special Identifiers
While a custom script is running, VLC will look for a number of different identifiers (names of functions or variables). How they are defined and implemented determines the look and functionality of a script, or whether the script runs at all. Different script types expect different identifiers to be defined, so see the type pages for more detail.

### Modules
In Lua, there are special tables called [Modules](https://www.lua.org/manual/5.1/manual.html#5.3). Modules are available via the global `vlc` table, depending on the type of script that is running.

| Name | Symbol(s) | Description | Availability |
| ---- | --------- | ----------- | ------------ |
| [Configuration](https://verghost.com/vlc-lua-docs/m/config) | `config` | Access and modify VLC configuration options | Extension, Interface |
| [Dialog](https://verghost.com/vlc-lua-docs/m/dialog) | `dialog` | Interface to the DialogUI object | Extension |
| [Equalizer](https://verghost.com/vlc-lua-docs/m/equalizer) | `equalizer` | Access and modify equalizer settings and presets | Interface |
| [GetText](https://verghost.com/vlc-lua-docs/m/gettext) | `gettext` | Alias for libvlc [gettext](https://en.wikipedia.org/wiki/Gettext) | Interface, Service Discovery |
| [Errno](https://verghost.com/vlc-lua-docs/m/errno) | `errno` | Error values | Extension, Interface |
| [HTTPd](https://verghost.com/vlc-lua-docs/m/httpd)  | `httpd` | Interface to the VLC HTTP Daemon constructor | Interface |
| [I/O](https://verghost.com/vlc-lua-docs/m/io)  | `io` | Input/Output (i.e. file read/write, directories, etc...) | Extension, Interface |
| [Messages](https://verghost.com/vlc-lua-docs/m/msg)  | `msg` | Output to the Messages console (Tools->Messages) | All types |
| [Miscellaneous](https://verghost.com/vlc-lua-docs/m/misc)  | `misc` | Uncategroized functionality | Interface |
| [Network](https://verghost.com/vlc-lua-docs/m/net)  | `net` | Various network methods | Extension, Interface |
| [Object](https://verghost.com/vlc-lua-docs/m/object)  | `object` | Provides access to various objects | Extension, Interface, Meta, Service Discovery |
| [OSD](https://verghost.com/vlc-lua-docs/m/osd)  | `osd` | On-screen display functionality (ex. Display OSD messages, modify channels) | Extension, Interface |
| [Player](https://verghost.com/vlc-lua-docs/m/input) | `player` | Access the VLC player interface | Extension, Interface, Service Discovery |
| [Playlist](https://verghost.com/vlc-lua-docs/m/playlist)  | `playlist` | Access and modify playlists | Extension, Interface |
| [Random](https://verghost.com/vlc-lua-docs/m/rand)  | `rand` | Get random numbers/bytes | Extension, Interface |
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
Outside of the modules in the global `vlc` table, VLC provides a few other useful Lua modules that offer some tools to aid in developing more complex scripts. These modules are found in VLC_INSTALL_PATH/lua/modules/ and must be explicitly required in lua code using the built-in [require](https://www.lua.org/pil/8.1.html) function.

```lua
require "module1" -- This works
local mod2 = require("module2") -- This also works
```

## LUAC
LUAC is a command line tool that lets you translate Lua scripts (.lua) into binary files (.luac). VLC will accept these files instead of the source code files. A more detailed description of LUAC can be found on it's [man page](https://www.lua.org/manual/5.1/luac.html), but here's a quick summary:

#### What LUAC does
- Precompiles Lua chunks into bytecode and saves them in a file, ensuring faster load times by saving on compilation time
- Adds resistance against small changes to a Lua program that might inadvertently change the program after it has been compiled

#### What LUAC does NOT do
- Create files that are necessarily smaller than the source code
- Speed up execution times or perform any optimizations that wouldn't already be done at runtime
- Apply any encryption or obfuscation that would prevent someone from easily reverse engineering Lua programs ([decompilers exist](http://luadec.luaforge.net/))
