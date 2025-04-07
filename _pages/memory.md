---
description: Using Memory API
---

# Memory

This example demonstrates how to allocate, read, write, and free memory in Lua.

```
-- Allocate a memory block of 64 bytes
local memory_handle = m.alloc(64)

-- Check if allocation was successful
if memory_handle ~= nil then
    engine.log("Memory allocated successfully!", 0, 255, 0, 255)

    -- Write values to the allocated memory
    m.write_int32(memory_handle, 0, 123456)       -- Write a 32-bit integer at offset 0
    m.write_float(memory_handle, 4, 3.14)        -- Write a float at offset 4
    m.write_double(memory_handle, 8, 2.71828)    -- Write a double at offset 8
    m.write_int8(memory_handle, 16, 127)         -- Write an 8-bit integer at offset 16

    -- Read values from the allocated memory
    local int_value = m.read_int32(memory_handle, 0)
    local float_value = m.read_float(memory_handle, 4)
    local double_value = m.read_double(memory_handle, 8)
    local int8_value = m.read_int8(memory_handle, 16)

    -- Log the values read from memory
    engine.log("Read int32: " .. int_value, 255, 255, 255, 255)
    engine.log("Read float: " .. float_value, 255, 255, 255, 255)
    engine.log("Read double: " .. double_value, 255, 255, 255, 255)
    engine.log("Read int8: " .. int8_value, 255, 255, 255, 255)

    -- Free the allocated memory
    m.free(memory_handle)
    engine.log("Memory freed successfully!", 0, 255, 0, 255)
else
    engine.log("Memory allocation failed!", 255, 0, 0, 255)
end
```

`m.alloc(size)`

Allocates a block of memory and returns a handle.



`m.free(handle)`

Frees an allocated memory block.



`m.write_int32(handle, offset, value)`

Writes a 32-bit integer to memory.



`m.write_float(handle, offset, value)`

Writes a float to memory.



`m.write_double(handle, offset, value)`

Writes a double to memory.



`m.write_int8(handle, offset, value)`

Writes an 8-bit integer to memory.



`m.read_int32(handle, offset)`

Reads a 32-bit integer from memory.



`m.read_float(handle, offset)`

Reads a float from memory.



`m.read_double(handle, offset)`

Reads a double from memory.



`m.read_int8(handle, offset)`

Reads an 8-bit integer from memory.



`m.read_string(handle, offset)`

Reads a string



`m.read_wide_string(handle, offset)`

Reads a unicode string



`m.write_string(handle, offset, str)`

Writes a string



`m.write_wide_string(handle, offset, str)`

Writes a unicode string



`m.get_size(handle)`

Gets current size of the buffer



**Example Usage:**

Allocates a memory block of 64 bytes.\
Writes different data types (integer, float, double, int8).\
Reads and logs the values stored in memory.\
Frees the allocated memory once done.
