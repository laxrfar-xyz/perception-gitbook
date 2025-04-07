---
description: Using the Input API
---

# Input System

This example demonstrates how to use input functions in Lua.

```
-- Check if a key is pressed and log it
function check_key_input()
    if input.is_key_pressed(32) then -- Spacebar key
        engine.log("Spacebar pressed!", 255, 255, 255, 255)
    end

    if input.is_key_down(17) then -- Ctrl key
        engine.log("Ctrl key is being held down!", 255, 255, 255, 255)
    end

    if input.is_key_toggled(20) then -- Caps Lock key
        engine.log("Caps Lock is toggled!", 255, 255, 255, 255)
    end
end

-- Get mouse position and movement delta
function check_mouse_input()
    local x, y = input.get_mouse_position()
    local dx, dy = input.get_mouse_move_delta()
    local scroll_delta = input.get_scroll_delta()

    engine.log("Mouse Position: " .. x .. ", " .. y, 255, 255, 255, 255)
    engine.log("Mouse Movement Delta: " .. dx .. ", " .. dy, 255, 255, 255, 255)
    engine.log("Mouse Scroll Delta: " .. scroll_delta, 255, 255, 255, 255)
end

-- Clipboard operations
function clipboard_example()
    local clipboard_text = input.get_clipboard()
    engine.log("Clipboard Content: " .. clipboard_text, 255, 255, 255, 255)

    input.set_clipboard("New Clipboard Data")
    engine.log("Clipboard updated!", 255, 255, 255, 255)
end

-- Menu and overlay handling
function menu_overlay_example()
    if input.is_menu_open() then
        engine.log("Menu is open!", 255, 255, 255, 255)
    else
        engine.log("Menu is closed!", 255, 255, 255, 255)
    end

    -- Force the cursor to remain active
    input.set_overlay_force_cursor_active(true)
    engine.log("Overlay cursor forced active!", 255, 255, 255, 255)
end

-- Register functions to be called every engine tick
engine.register_on_engine_tick(function()
    check_key_input()
    check_mouse_input()
    menu_overlay_example()
end)
```

`input.simulate_mouse(dx, dy, flag)`

Simulate mouse input using location or flags



`input.simulate_keyboard(key, flag)`

Simulate keyboard input using vk and flags



`input.is_key_pressed(key)`

Detects if a key is pressed once.



`input.is_key_down(key`

Detects if a key is being held down.



`input.is_key_toggled(key)`

Checks if a key’s toggle state is active



`input.get_mouse_position()`

Returns the mouse’s current position (`x, y`).



`input.get_mouse_move_delta()`

Returns the mouse movement delta (`dx, dy`).



`input.get_scroll_delta()`

Returns the mouse scroll wheel delta.



`input.get_clipboard()`

Gets the clipboard content.



`input.set_clipboard(text)`

Sets new text to the clipboard.



`input.is_menu_open()`

Checks if the menu is open.



`input.set_overlay_force_cursor_active(state)`

Forces the overlay cursor to be active (`true`) or inactive (`false`).



**Example Usage:**

Detects and logs key presses (`Spacebar`, `Ctrl`, `Caps Lock`).\
Logs the mouse position, movement delta, and scroll wheel changes.\
Retrieves and modifies the clipboard content.\
Checks if the menu is open and forces the cursor to remain active.
