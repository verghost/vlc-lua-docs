---
title: Equalizer Module
project: vlc-lua-docs
---
Provides access to VLC's [equalizer](https://en.wikipedia.org/wiki/Equalization_(audio)) (Tools->Effects and Filters->Audio Effects->Equalizer).  
Control EQ, levels and preamp settings. Each EQ componenet has methods that can modify them.

# Availability

| Script Types |
| ------------ |
| [Interface](../../t/intf) |

----
## `enable()`
Turn equalizer on or off.

### Usage
```lua
if eq_should_die then
  vlc.equalizer.enable(false)
end
```

### Parameters
- `state` Boolean indicating whether the EQ should be enabled

----
# Preamplifier
The following methods control the EQ [preamp](https://en.wikipedia.org/wiki/Preamplifier).


## `preampget()`
Retrieve the current EQ preamp level, which is measured in decibels.

### Usage
```lua
local level = vlc.equalizer.preampget()
```

### Return value
A float representing the preamplification level in Decibels.

----
## `preampset()`
Set the EQ preamp level.

### Usage
```lua
local level = 12.0
vlc.equalizer.preampset(level) -- set preamp to 12db
```

### Parameters
- `level` Float representing the new level in decibels; a number between -20.0 and 20.0

----
# Equalizer Bands
The EQ is composed of several "bands", each of which modify a different frequency range. Each EQ band is asssigned an ID number:

| Band ID | Frequency |
| ------- | --------- |
| 0 | 60 Hz |
| 1 | 170 Hz |
| 2 | 310 Hz |
| 3 | 600 Hz |
| 4 | 1 kHz |
| 5 | 3 kHz |
| 6 | 6 kHz |
| 7 | 12 kHz |
| 8 | 14 kHz |
| 9 | 16 kHz |

----
## `equalizerget()`
Get EQ levels for all bands as a table. 

### Usage
```lua
local levels_table = vlc.equalizer.equalizerget()
for id,level in pairs(levels_table) do
  print("EQ @" .. id .. " is: " .. level)
end
```

### Return value
Table representing the band levels of the equalzer

----
## `equalizerset()`
Set EQ levels for a specified band.

### Usage
```lua
local new_4_level = 12.4
vlc.equalizer.equalizerset(4, new_4_level)
```

### Parameters
- `id` The band ID; an integer between 0-9 (inclusive)
- `level` (Float) New level for the specified band in decibels; a number between -20.0 and 20.0

----
# Presets
The VLC EQ supports presets, which allows users to save their custom EQ settings.


## `presets()`
Get the names of available EQ presets.

### Usage
```lua
local presets = vlc.equalizer.presets()
for i,p in pairs(presets) do
  print("Preset with ID #" .. i .. " is called " .. p)
end
```

### Return value
Table containing the names of available EQ presets

----
## `setpreset()`
Set the EQ to a specified preset.

### Parameters
- `id` Integer pointing to position of the preset in the preset list (found programatically with [`presets()`](#presets-1)). Must be greater than 0 and less than the total number of presets
