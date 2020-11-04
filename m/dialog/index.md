---
title: Dialog Module
project: vlc-lua-docs
---
This module provides access to VLC's dialog and widget system via the UI Dialog object.

# Availability

| Script Types |
| ------------ |
| [Extension](../../t/extensions) |

----
# UI Dialog Object
This is the table that represents the VLC dialog, of which there can be only one per extension. Functionality can be added via "widgets", which have their own class.


## `dialog()`
Constructor for the UI Dialog object.

### Usage
```lua
local dlg = vlc.dialog(title)
```
### Parameters
- `title`
String representing the title of the new dialog

### Return value
A table representing the new created dialog

----
## `dialog:show()`
Show the dialog, create the window.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
dlg:show()
```

----
## `dialog:hide()`
Hide dialog without closing it.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
dlg:show()
...
if should_hide then
  dlg:hide()
end
```

----
## `dialog:delete()`
Close the dialog and delete it.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
...
if closing_time then
  dlg:delete()
end
```

----
## `dialog:set_title()`
Change the title of the dialog.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
dlg:set_title(title)
```
### Parameters
- `title` A string representing the new dialog title

----
## `dialog:update()`
Updates the dialog without waiting for the current function to complete.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
dlg:update()
```

----
## `dialog:del_widget()`
Delete a widget from the dialog.  
This will always cause an update; repositioning may occur.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
...
if should_delete_widget then
  dlg:del_widget(widget)
end
```
### Parameters
- `widget` The widget to be deleted

----
# Adding Widgets
Widgets are small components that provide most of utility and U.I. of the dialog window. They are added by calling the `add_` methods of the dialog object. The widgets are arranged according to a grid/table system, with each widget on a specific column and row.

## Widget Types

| Type | Add Method | Widget Methods |
| ---- | ---------- | -------------- |
| Button | [add_button()](#dialogadd_button) | [get_text()](#widgetget_text), [set_text()](#widgetset_text) |
| Label | [add_label()](#dialogadd_label) | [get_text()](#widgetget_text), [set_text()](#widgetset_text) |
| HTML | [add_html()](#dialogadd_html) | [get_text()](#widgetget_text), [set_text()](#widgetset_text) |
| Text Input | [add_text_input()](#dialogadd_text_input) | [get_text()](#widgetget_text), [set_text()](#widgetset_text) |
| Password | [add_password()](#dialogadd_password) | [get_text()](#widgetget_text), [set_text()](#widgetset_text) |
| Check Box | [add_check_box()](dialogadd_check_box) | [get_text()](#widgetget_text), [set_text()](#widgetset_text), [get_checked()](#widgetget_checked), [set_checked()](#widgetset_checked) |
| Dropdown | [add_dropdown()](#dialogadd_dropdown) | [clear()](#widgetclear), [get_value()](#widgetget_value), [add_value()](#widgetadd_value) |
| List | [add_list()](dialogadd_list) | [get_selection()](#widgetget_selection), [clear()](#widgetclear), [get_value()](#widgetget_value) (4.0+), [add_value()](#widgetadd_value) (4.0+) |
| Image | [add_image()](#dialogadd_image) | None |
| Spin Icon | [add_spin_icon()](#dialogadd_spin_icon) | [animate()](#widgetanimate), [stop()](#widgetstop) |

----
## Widget Parameters
These are optional when creating a new widget, but can be specified to customize arrangments and widget sizes.
Here they are, in order:

- `col` The column of the grid the widget sits in; default is 1
- `row` The row of the grid the widget sits in; default is the # of rows
- `hspan` The horizontal span of columns the widget inhabits
- `vspan` The vertical span of rows the widget inhabits
- `width` Width hint value in pixels; suggests the width you want for the widget
- `height` Height hint value in pixels; suggests the height you want for the widget

### Things to note:
1. Lua indexes values starting at 1, not 0; this is the case for `row` and `col`.
2. Different widgets use and discard values internally depending on what type of widget it is (hint values get discarded often). I'd like to document their usage at some point, but for now see the [source code](https://code.videolan.org/videolan/vlc/-/tree/master/modules/gui/qt/dialogs/extensions) for specifics.

----
## `dialog:add_button()`
Add a button widget to the dialog.

### Usage
```lua
function clickme()
  -- do stuff
end
...
local dlg = vlc.dialog("My VLC Extension")
local button_wgt = dlg:add_button("Click Me", clickme, ...)
```
### Parameters
- `text` String representing the text displayed on the button
- `func` Reference to the function that should be called when the button is clicked
- Optional
  - `...` [Widget](#widget-parameters) parameters

### Return value
A widget object corresponding to the new widget  
This widget provides the following methods: [get_text()](#widgetget_text), [set_text()](#widgetset_text)

----
## `dialog:add_label()`
Add a text label widget to the dialog.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
local label_wgt = dlg:add_label("My label", ...)
```

### Parameters
- `text` String representing the text to be dsiplayed on the label
- Optional
  - `...` [Widget](#widget-parameters) parameters

### Return value
A widget object corresponding to the new widget  
This widget provides the following methods: [get_text()](#widgetget_text), [set_text()](#widgetset_text)

----
## `dialog:add_html()`
Add a rich text label widget, formatted with basic HTML (i.e. `<i>`, `<h1>`), to the dialog.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
local rich_wgt = dlg:add_html("My rich label with <i>cool</i> HTML!", ...)
```

### Parameters
- `text` String representing the content to be dsiplayed on the label
- Optional
  - `...` [Widget](#widget-parameters) parameters

### Return value
A widget object corresponding to the new widget  
This widget provides the following methods: [get_text()](#widgetget_text), [set_text()](#widgetset_text)

----
## `dialog:add_text_input()`
Add an editable text input box to the dialog.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
local input_wgt = dlg:add_text_input("This is a Text Box", ...)
```

### Parameters
- `text` String representing the text to be placed in the text input
- Optional
  - `...` [Widget](#widget-parameters) parameters

### Return value
A widget object corresponding to the new widget  
This widget provides the following methods: [get_text()](#widgetget_text), [set_text()](#widgetset_text)

----
## `dialog:add_password()`
Add an editable text field to the dialog.  
Text input will be displayed with characters replaced with '*'.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
local passwd_wgt = dlg:add_password("password123", ...)
```

### Parameters
- `text` String representing the default text value in the field
- Optional
  - `...` [Widget](#widget-parameters) parameters

### Return value
A widget object corresponding to the new widget  
This widget provides the following methods: [get_text()](#widgetget_text), [set_text()](#widgetset_text)

----
## `dialog:add_check_box()`
Add a check box widget to the dialog.  
Check box stores a true/false state and is accompanied by a text label.
### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
local check_wgt = dlg:add_check_box("Yes or No?", false, ...)
```

### Parameters
- `text` String representing the text to be dsiplayed on the accompanying text label
- Optional
  - `checked` Boolean representing the default state of the check box; parameter defaults to `false`
  - `...` [Widget](#widget-parameters) parameters

### Return value
A widget object corresponding to the new widget  
This widget provides the following methods: [get_text()](#widgetget_text), [set_text()](#widgetset_text), [get_checked()](#widgetget_checked), [set_checked()](#widgetset_checked)

----
## `dialog:add_dropdown()`
Add a dropdown list widget to the dialog.  
Only one item can be selected at a time. Items are managed using [add_value()](#widgetadd_value), [clear()](#widgetclear) and [get_value()](#widgetget_value).

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
local drop_wgt = dlg:add_dropdown(...)
```

### Parameters
- Optional
  - `...` [Widget](#widget-parameters) parameters

### Return value
A widget object corresponding to the new widget  
This widget provides the following methods: [clear()](#widgetclear), [get_value()](#widgetget_value), [add_value()](#widgetadd_value)

----
## `dialog:add_list()`
Add a list widget to the dialog.  
One or multiple items can be selected at a time, items are added to the list from widget methods.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
local list_wgt = dlg:add_list(...)
```

### Parameters
- Optional
  - `...` [Widget](#widget-parameters) parameters

### Return value
A widget object corresponding to the new widget  
This widget provides the following methods: [get_selection()](#widgetget_selection), [clear()](#widgetclear), [get_value()](#widgetget_value) (4.0+), [add_value()](#widgetadd_value) (4.0+)

----
## `dialog:add_image()`
Add an image label widget to the dialog.  
Image path is absolute or relative on the local machine.

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
local img_wgt = dlg:add_image("C:\\some\\path\\image.ext", ...)
```

### Parameters
`path` String representing the path to the image
- Optional
  - `...` [Widget](#widget-parameters) parameters

### Return value
A widget object corresponding to the new widget

----
## `dialog:add_spin_icon()`
###### Only available in VLC v4.0+
Add a spin icon widget to the dialog.  

### Usage
```lua
local dlg = vlc.dialog("My VLC Extension")
local spin_icon_wgt = dlg:add_spin_icon(0, ...)
```

### Parameters
`loop_count` Integer corresponding to the loop count to play: 0->
- Optional
  - `...` [Widget](#widget-parameters) parameters

### Return value
A widget object corresponding to the new widget  
This widget provides the following methods: [animate()](#widgetanimate), [stop()](#widgetstop)

----
# Modifying Widgets
Widget objects have their own methods thatcan get and modify their data. The methods that are available differ depending on the widget type.

----
## `widget:get_text()`
Get text displayed by the widget.  
Applies to the follwing types of widget: button, label, html, text_input, password and check_box.

### Usage
```lua
local wgt = dialog:add_check_box("Yes/No")
vlc.msg.info(wgt:get_text()) -- "Yes/No"
```

### Return value
A string containing the display text for the widget

----
## `widget:set_text()`
Change the text displayed by the widget.  
Applies to the follwing types of widget: button, label, html, text_input, password and check_box.

### Usage
```lua
local wgt = dialog:add_check_box("Yes/No")
wgt:set_text("No/Yes")
```

### Parameters
- `text` String representing the new display text for the widget

----
## `widget:get_checked()`
Get the true/false state of the widget.  
Applies to the follwing types of widget: check_box.

### Usage
```lua
local wgt = dialog:add_check_box("Yes/No", true)
local currState = wgt:get_checked() -- true
```

### Return value
A boolean value representing the current true/false state of the widget

----
## `widget:set_checked()`
Change the true/false state of the widget.  
Applies to the follwing types of widget: check_box

### Usage
```lua
local wgt = dialog:add_check_box("Yes/No")
wgt:set_checked(true)
```

### Parameters
`checked` Boolean representing the new true/false state of the widget

----
## `widget:get_value()`
Get the value corresponding to the current selected item in the widget.  
Applies to the follwing types of widget: dropdown and list (4.0+).

### Usage
```lua
local ddv1, ddv2 = dialog:add_dropdown():get_value()
ddv1 -- -1
ddv2 -- nil
```

### Return value
An Integer corresponding to the identifier selected item
AND
A string (or nil) representing the text value of the selected item

----
## `widget:add_value()`
Add an item to the widget  
Applies to the follwing types of widget: dropdown and list.

### Usage
```lua
local dropdown_wgt = dialog:add_dropdown()
dropdown_wgt:add_value("four", 4)
```

### Parameters
- `text` String text display value for the item
- Optional
	- `id` Integer identifier for the new item (Defaults to 0)
		- If two items share the same id, then widget:get_value will fail on the item

----
## `widget:clear()`
Clear all items in the widget, deleting them.  
Applies to the follwing types of widget: dropdown and list.

### Usage
```lua
local dropdown_wgt = dialog:add_dropdown()
...
if clear_list then
  dropdown_wgt:clear()
end
```

----
## `widget:get_selection()`
Get the current selection for the widget.  
Applies to the follwing types of widget: list.

### Usage
```lua
local list_wgt = dialog:add_list()
local lsel = list_wgt:get_selection() -- empty table
```

### Return value
Table corresponding to any selected items; Keys = Integer IDs, Values = String text value

----
## `widget:animate()`
###### Only in 4.0+
Start the animation on the widget.  
Applies to the follwing types of widget: spin_icon.

----
## `widget:stop()`
###### Only in 4.0+
Stop an animation in progress on the widget.
Applies to the follwing types of widget: spin_icon.
