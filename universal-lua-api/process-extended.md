---
description: Extended Proc API – Attach to a Process
---

# Process - Extended

This introduces three new functions to the **proc API**, allowing you to attach to a process using its **PID**, **name**, or **window properties**.\
Once attached, you can use other **proc API** functions for memory operations.

This does not create any handles do not mistake this with OpenProcess



**Attaching to a Process**

You can attach using a **Process ID (PID)**, **process name**, or **window class + name**.

```
-- Attempt to attach to Notepad by process name
if not proc.attach_by_name("notepad.exe") then
    engine.log("Failed to attach to Notepad!", 255, 0, 0, 255)
    return
end
engine.log("Successfully attached to Notepad!", 0, 255, 0, 255)
-- Get the base address of Notepad
local base_address = proc.base_address()
if base_address == nil then
    engine.log("Failed to get Notepad base address!", 255, 0, 0, 255)
    return
end
engine.log("Base Address: " .. string.format("0x%X", base_address), 255, 255, 255, 255)
-- Define the offset for e_lfanew in the DOS header
local e_lfanew_offset = 0x3C
-- Read the e_lfanew value (DWORD) from the PE header
local e_lfanew = proc.read_int32(base_address + e_lfanew_offset)
if e_lfanew == nil then
    engine.log("Failed to read e_lfanew!", 255, 0, 0, 255)
    return
end
engine.log("e_lfanew: " ..e_lfanew, 0, 255, 0, 255)
```

`proc.attach_by_pid(process_id, has_corrupt_cr3)`

Attach using a **process ID (integer)**



`proc.attach_by_name(process_name, has_corrupt_cr3)`

Attach using a **process name (string)**.



`proc.attach_by_window(window_class, window_name, has_corrupt_cr3)`

Attach using a **window class and window name (both strings)**.



`proc.is_attached()`

Check if the attachment was successful.

After attaching, you can use other **proc API functions** to interact with process memory.



has\_corrupt\_cr3 is optional but a must requirement for games protected by easy anti cheat. This is required to resolve corrupted cr3.



**Notes:**

These functions **do not create OpenProcess handles**, they only set up process interaction.

If an invalid argument is provided, an error is thrown.

If the process cannot be found or attached, the function returns an error.
