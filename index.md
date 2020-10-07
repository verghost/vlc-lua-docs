# VLC Lua Docs
These are docs intended to help with creating custom Lua scripts to extend VLC functionality.

#### **Disclaimers**
1. I might refer to "lists", "arrays" or "objects" a lot in these docs, but that is by habbit. In lua these are all just [tables](https://www.lua.org/pil/11.html). Bascially, this is NOT in any way a Lua tutorial.
2. All info in these docs is sourced from [README files in here](https://code.videolan.org/videolan/vlc/-/tree/master/share/lua/), [VideoLAN Forums](https://forum.videolan.org/), [the Wiki](https://wiki.videolan.org/), [code from existing VLC addons](https://addons.videolan.org) and of course my own tinkering and looking at the source code.

## How to install custom Lua scripts
Lua scripts are installed in the /Lua folder of the VLC install directory under subdirectories according to their type
- Windows (all users): %ProgramFiles%\VideoLAN\VLC\lua\
- Windows (current user): %APPDATA%\VLC\lua\
- Linux (all users): /usr/lib/vlc/lua/
- Linux (current user): ~/.local/share/vlc/lua/
- Mac OS X (all users): /Applications/VLC.app/Contents/MacOS/share/lua/
- Mac OS X (current user): /Users/%your_name%/Library/Application Support/org.videolan.vlc/lua/

## Types of scripts
There are a few different types of lua scripts, each with their own purpose, functionality and install directory
- Interfaces (/lua/intf)
- Extensions  (/lua/extensions)
- Meta Scripts
  - Art (/lua/meta/art)
  - Fetcher (/lua/meta/fetcher)
  - Reader (/lua/meta/reader)
- Playlist parsers (/lua/playlist)
- Services Discovery (/lua/sd)

## Modules
In Lua, there are special tables called [Modules](https://www.lua.org/manual/5.1/manual.html#5.3) that work kind of like "libraries" do in other languages (this might be why, with a few exceptions, they're implemented in VLC source code under [libs](https://code.videolan.org/videolan/vlc/-/blob/master/modules/lua/libs)). Normally the programmer would use the `require` keyword to include modules in their code, but VLC's Lua environment does the requiring on it's end. Modules are available via the global `vlc` table, depending on the type of script that is running.

| Name | Symbol(s) | Description | Availability |
| ---- | --------- | ----------- | ------------ |
| [Configuration](https://verghost.com/vlc-lua-docs/config) | `config` | Access and modify VLC configuration options | Extension, Interface |
| [Dialog](https://verghost.com/vlc-lua-docs/dialog) | `dialog` | Interface to the DialogUI object | Extension |
| [Equalizer](https://verghost.com/vlc-lua-docs/equalizer) | `equalizer` | Access and modify equalizer settings and presets | Interface |
| [GetText](https://verghost.com/vlc-lua-docs/iandl) | `gettext` | Alias for libvlc [gettext](https://en.wikipedia.org/wiki/Gettext) | Interface, Service Discovery |
| [Errno](https://verghost.com/vlc-lua-docs/errno) | `errno` | Error values | Extension, Interface |
| [HTTPd](https://verghost.com/vlc-lua-docs/httpd)  | `httpd` | Interface to the VLC HTTP Daemon constructor | Interface |
| [Input/Output](https://verghost.com/vlc-lua-docs/io)  | `io` | Input/Output (i.e. file read/write, directories, etc...) | Extension, Interface |
| [Messages](https://verghost.com/vlc-lua-docs/msg)  | `msg` | Output to the Messages console (Tools->Messages) | All types |
| [Miscellaneous](https://verghost.com/vlc-lua-docs/misc)  | `misc` | Uncategroized functionality | Interface |
| [Network](https://verghost.com/vlc-lua-docs/net)  | `net` | Various network methods | Interface and Extension |
| [Object](https://verghost.com/vlc-lua-docs/object)  | `object` | Provides access to various objects | Extension, Interface, Meta, Service Discovery |
| [OSD](https://verghost.com/vlc-lua-docs/osd)  | `osd` | On-screen display functionality (ex. Display OSD messages, modify channels) | Extension, Interface |
| [Player](https://verghost.com/vlc-lua-docs/player)  | `player` | Interface to VLC player | Unknown |
| [Playlist](https://verghost.com/vlc-lua-docs/playlist)  | `playlist` | Access and modify playlists | Unknown |
| [Random](https://verghost.com/vlc-lua-docs/rand)  | `rand` | Get random numbers/bytes | Unknown |
| [Services discovery](https://verghost.com/vlc-lua-docs/sd)  | `sd` | Functions for service discovery scripts (i.e. add nodes, items) | Interface, Service Discovery |
| [Stream](https://verghost.com/vlc-lua-docs/stream)  | `stream`, `memory_stream`, `directory_stream` | Access to data streams and methods to read/modify them | Interface |
| [Strings](https://verghost.com/vlc-lua-docs/strings)  | `strings` | String utils (ex. parse URI/URL, handle special chars) | Interface |
| [Variables](https://verghost.com/vlc-lua-docs/var)  | `var` | Interface to VLC internal variables(?) | Unknown |
| [Video](https://verghost.com/vlc-lua-docs/video)  | `video` | Change video interface | Unknown |
| [VLM](https://verghost.com/vlc-lua-docs/vlm)  | `vlm` | VideoLAN Manager object instance method | Unknown |
| [Volume](https://verghost.com/vlc-lua-docs/volume)  | `volume` | Modify volume | Extension, Interface |
| [Windows](https://verghost.com/vlc-lua-docs/win)  | `win` | Access to Windows console | Extension, Interface (Windows builds only) |
| [XML](https://verghost.com/vlc-lua-docs/xml)  | `xml` | [XML](https://en.wikipedia.org/wiki/XML) reader | All types |

## Special Functions
While a custom script is running, a number of different functions are called by VLC. These functions are expected to be defined by the custom script and are often necessary if a script is to work properly. For some of these functions, there are return values that VLC expects while others can be thought of like [DOM events](https://developer.mozilla.org/en-US/docs/Web/Events), which are called by VLC when some action takes place in the main program. Like with Modules, different types of scripts require different function definitions. Like modules, these special functions differ by the type of script.

## Luac
Luac is a command line tool that lets you compile Lua scripts.
