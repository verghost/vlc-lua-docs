---
title: Extension Scripts
project: vlc-lua-docs
---
Extension scripts are smaller applications that "extend" VLC functionality. To this end, the extension scripts are the only kind that have access to the [dialog lua module](/vlc-lua-docs/m/dialog), which allows developers to create a new dialog window.

Extension scripts are not run on VLC startup, instead they are launched (or "activated") via the *View* menu.

