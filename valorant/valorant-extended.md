---
description: Valorant - Class Offset Dumping
---

# Valorant - Extended

`valorant.get_class_dump(pointer)`

**Description**

Returns a table containing the class fields for the specified class pointer in Valorant. Each entry in the table includes:\
**name** (_string_) – The name of the class field.\
**offset** (_integer_) – The memory offset associated with the field.

This is useful for reverse engineering or understanding the internal structure of class objects at runtime.

**Arguments**

**pointer** (_integer_) – The memory address of the class you want to dump.

**Return Type**

```
{
    [1] = { name = "PlayerCameraManager::CameraCachePrivate", offset = 0x120 },
    [2] = { name = "Character::Mesh", offset = 0x154 },
    ...
}
```

Returns **nil** and logs an error if:\
Argument is missing or not an integer.\
Pointer is null.\
Dump is empty.

**Example Usage**

```
local pointer = 0x1A2B3C4D  -- Replace with actual class pointer (For example uworld)
local dump = valorant.get_class_dump(pointer)

if dump == nil then
    engine.log("Class dump failed.", 255, 0, 0, 255)
    return
end

for i, entry in ipairs(dump) do
    engine.log(string.format("%s = 0x%X", entry.name, entry.offset), 0, 255, 0, 255)
end
```

**File Dump Example**

To save the class dump to _class\_dump.txt_ using the filesystem API:

```
local pointer = 0x1A2B3C4D  -- Replace with actual class pointer (For example uworld)
local dump = valorant.get_class_dump(pointer)

if dump == nil then
    engine.log("Class dump failed.", 255, 0, 0, 255)
    return
end

local lines = {}

for i, entry in ipairs(dump) do
    table.insert(lines, string.format("%s = 0x%X", entry.name, entry.offset))
end

local text = table.concat(lines, "\n")

fs.write_to_file("class_dump.txt", text)
engine.log("Class dump written to class_dump.txt", 0, 255, 0, 255)
```
