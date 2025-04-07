---
description: Using Process API
---

# Process

This example demonstrates how to interact with a process's memory in Lua.

```
-- Check if a process is attached
if proc.is_attached() then
    engine.log("Process is attached!", 0, 255, 0, 255)

    -- Get process details
    local process_id = proc.pid()
    local process_base = proc.base_address()
    local main_module, module_size = proc.get_base_module()

    engine.log("Process ID: " .. process_id, 255, 255, 255, 255)
    engine.log("Base Address: " .. process_base, 255, 255, 255, 255)
    engine.log("Main Module: " .. main_module .. " | Size: " .. module_size, 255, 255, 255, 255)

    -- Find a module by name
    local module_base, module_size = proc.find_module("example.dll")
    if module_base ~= nil then
        engine.log("Module 'example.dll' found at: " .. module_base, 0, 255, 0, 255)
    else
        engine.log("Module 'example.dll' not found!", 255, 0, 0, 255)
    end

    -- Read and write process memory
    local address = process_base + 0x1000  -- Example offset
    local original_value = proc.read_int32(address)
    engine.log("Original Value: " .. original_value, 255, 255, 255, 255)

    proc.write_int32(address, 99999)  -- Modify memory value
    engine.log("Modified Value: " .. proc.read_int32(address), 0, 255, 0, 255)

    -- String manipulation
    local str_address = process_base + 0x2000  -- Example string address
    local read_str = proc.read_string(str_address, 20)
    engine.log("Read String: " .. read_str, 255, 255, 255, 255)

    proc.write_string(str_address, "New String")
    engine.log("String Written Successfully!", 0, 255, 0, 255)

    -- Cleanup check
    if proc.did_exit() then
        engine.log("Attached process has exited!", 255, 0, 0, 255)
    end
else
    engine.log("No process is attached!", 255, 0, 0, 255)
end
```

`proc.is_attached()`

Checks if a process is currently attached.



`proc.did_exit()`

Checks if the attached process has exited.



`proc.pid()`

Retrieves the attached process ID.



`proc.base_address()`

Returns the base address of the attached process.



`proc.get_base_module()`

Gets the base module’s address and size



`proc.find_module(module_name)`

Finds a module by name and returns its base address and size.



`proc.read_int32(address)`

Reads a 32-bit integer from memory.



`proc.write_int32(address, value)`

Writes a 32-bit integer to memory.



`proc.read_string(address, size)`

Reads a string from memory.



`proc.write_string(address, text)`

Writes a string to memory.



**Example Usage:**

Retrieves process ID, base address, and module information.\
Finds a specific module and logs its address.\
Reads an integer from memory, modifies it, and logs the new value.\
Reads and writes a string in process memory.\
Checks if the attached process has exited.
