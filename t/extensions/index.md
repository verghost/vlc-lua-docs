---
title: Extension Scripts
project: vlc-lua-docs
---
Extension scripts are smaller applications that "extend" VLC functionality. To this end, the extension scripts are the only kind that have access to the [dialog lua module](/vlc-lua-docs/m/dialog), which allows developers to create a new dialog window.

Extension scripts are not activated by default on startup, this must be done via the *View* menu.

# Extension Functions

## `vlc.deactivate()`
Deactivates extension

----
## `vlc.keep_alive()`
Keep an extension alive. This resets the watch timer to 0.

----
# Special Functions
When extension scripts are started VLC looks for a few functions, some of which are necessary for the script to continue execution.  
These functions might be required to accept parameters and/or return specific values.

## `descriptor()`
This is one of the most important special functions, expected in most VLC Lua scripts. In extensions, it is a required for the extension to be registered by VLC.  

### Return value
This function only needs to return a table of information, which can have the following fields:

- `title` This is the title of the extension and the only mandatory field
- `author` Author of the extension
- `shortdesc` Short description (If this is not provided, then the first line of description will be used for short description in *Tools*->*Plugins and extensions* menu)
- `description` Full description
- `url` Website or other URL associated with the extension (i.e. github link, personal website, etc...)
- `version` Version string
- `icon` Extension icon
- `capabilities` A list containing one or more of the following strings, each of which will tell VLC what functionality to enable (or disable) for the extension
	- "menu": Tells VLC to call menu() and set up menu options to call trigger_menu()
	- "trigger": Tells VLC to call trigger() and to NOT call activate()
	- "input-listener": Tells VLC to call input_changed()
	- "meta-listener": Tells VLC to call meta_changed()
	- "playing-listener": Tells VLC to call status_changed()

----
## `activate()`
Called when the extension is started via the *View* menu.

----
## `menu()`
Defines the *View* menu options that is available once the extension is activated.

### Return value
A list of strings representing the menu options to be displayed

----
## `trigger_menu()`
Called when a menu option is selected.

### Parameters
- `id` Menu identifier; the index of the selected menu item in the list returned by menu()

----
## `input_changed()`
Called when the input item has changed (e.g. When a new song is playing).

----
## `meta_changed()`
Called when metadata in the player has changed.

----
## `status_changed()`
Called when player status changes.

----
## `close()`
Called when the extension dialog is closed by the user (i.e. by exiting out of the dialog).  
Not called when the extension is deactivated via the *View* menu.

----
## `trigger()`
Called when the extension is started via the *View* menu and "trigger" was supplied in the extension's [`descriptor()`](#descriptor).

----
## `deactivate()`
Called when the extension is deactivated via the *View* menu.

----
# Example

Here is an sample extension.

```lua
-- Sample Extension

ext_title = "ext-Sample"
selected_item = ""
menu_items = {"Item 1", "Item 2", "Item 3", "Item 4"}

-- Descriptor: VLC looks for this to provide meta info about our extension
function descriptor()
	return {
		title = ext_title,
		version = "0.1",
		author = "verghost",
		url = 'https://github.com/verghost/vlc-lua-docs',
		description = "A Sample extension that does sample related things.",
		capabilities = {"menu", "input-listener"}
	}
end

function set_selection(s)
	selected_item = tostring(s)
	lbl_wgt:set_text("You have selected: " .. selected_item)
end

-- Callback function for the "Click Me" button
function click()
	local l1, l2 = dropd_wgt:get_value()
	set_selection(l2)
end

function activate()
	main_dlg = vlc.dialog(ext_title)
	
	-- VLC will always try to shrink the dialog window, so always define your col, row, hspan and vspan.
	main_dlg:add_label("Welcome to the Sample Extension!", 1, 1, 8, 1)
	
	-- add dropdown
	dropd_wgt = main_dlg:add_dropdown(1, 2, 8, 1)
	for i,e in pairs(menu_items) do
		dropd_wgt:add_value(e, i-1)
	end
	
	-- Add a label
	lbl_wgt = main_dlg:add_label("No item selected", 1, 3, 8, 1)
	main_dlg:add_button("Click Me", click)
	
	main_dlg:show() -- Once we've finished setting up our dialog, we make it visible
end

-- Called when the dialog window is closed
function close()
	vlc.deactivate() -- call deactivate() here, assuming that the extension should also be deactivated when the main dialog box closes
end

-- Called by vlc to get menu options
function menu()
	return menu_items
end

-- this function recieves the index of the chosen menu item
function trigger_menu(id)
	set_selection(menu_items[id])
end

-- input listener
function input_changed()
	vlc.msg.info("Input changed!")
end

-- Called when the extension is deactivated.
-- Deactivation closes the menu and stops the extension script entirely
function deactivate()
	main_dlg:delete() -- if we're deactivating, we should destroy our dialog
end
```