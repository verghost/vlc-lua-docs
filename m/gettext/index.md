---
title: GetText Module
project: vlc-lua-docs
---

This modules allows access to the [gettext](https://en.wikipedia.org/wiki/Gettext) system implementation provided by VLC.  

----
## `_()`
[Localization](https://en.wikipedia.org/wiki/Internationalization_and_localization) function for the module.  
The name comes from the tendancy for the C function "gettext()" to be aliased to "_" to save space.  

### Usage
```lua
-- VLC language is set to: "Français"
local search = vlc.gettext._("Search")
print(search) -- Outputs "Rechercher"
```

### Parameters
- `str` A string to be localized to the current user's language

### Return value
A localized string in the user's language

----
## `N_()`
Returns a string passed to it.  
The name seems to refer to the [plural form](https://en.wikipedia.org/wiki/Gettext#Plural_form) of gettext, but `N_` is not called [internally](https://code.videolan.org/videolan/vlc/-/blob/master/modules/lua/libs/gettext.c).

```lua
-- VLC language is set to: "Français"
local search = vlc.gettext.N_("Search")
print(search) -- Outputs "Search"
```

### Parameters
- Optional
  - `str` A string to be returned

### Return value
If `str` is passed, then it is returned, otherwise `nil`.
