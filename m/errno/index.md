---
title: ErrNo Module
project: vlc-lua-docs
---

When calling a vlc method, sometimes error codes can be returned. This module provides access to a list of these potential error numbers/codes. So far, these (as far as I know) are only useful for the [IO module](../io).
List of error values:

- `vlc.errno.ENOENT` No such file or directory
- `vlc.errno.EEXIST` File exists already
- `vlc.errno.EACCES` Permission denied
- `vlc.errno.EINVAL` Invalid argument

## Example
```lua
local c1, c2 = vlc.io.unlink("/this/path/does/not/exist/file.txt")
if c1 == -1 then -- operation failed
  if c2 == vlc.errno.ENOENT then
    print("Oh no: No such file or directory")
...
```
