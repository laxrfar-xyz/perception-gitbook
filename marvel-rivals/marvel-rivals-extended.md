---
description: Marvel Rivals - Extended API (marvel_rivals)​
---

# Marvel Rivals - Extended

`marvel_rivals.get_local_player()`

Returns a table with:

`player_controller`, `skeletal_mesh`, `root_component`, `child_actor_component`, `child_actor`,\
`bone_array`, `health_component`, `player_state`, `pawn`, `hero_name`,\
plus individual `bone_id_*` values (e.g., `bone_id_head`, `bone_id_chest`, etc.)\


`marvel_rivals.get_player_list()`

Returns a table of players, each containing:\
`skeletal_mesh`, `root_component`, `child_actor_component`, `child_actor`,\
`bone_array`, `health_component`, `player_state`, `pawn`, `hero_name`,\
plus `bone_id_*` values for each relevant bone.



**Bone IDs**

`bone_id_upper_head`\
`bone_id_head`\
`bone_id_neck`\
`bone_id_chest`\
`bone_id_stomach`\
`bone_id_pelvis`



Left Arm

`bone_id_left_shoulder`\
`bone_id_left_elbow`\
`bone_id_left_hand`



Right Arm

`bone_id_right_shoulder`\
`bone_id_right_elbow`\
`bone_id_right_hand`



Left Leg

`bone_id_left_shoulder`\
`bone_id_left_elbow`\
`bone_id_left_hand`



Right Arm

`bone_id_right_shoulder`\
`bone_id_right_elbow`\
`bone_id_right_hand`



Left Leg

`bone_id_left_hip`\
`bone_id_left_knee`\
`bone_id_left_foot`



Right Leg

`bone_id_right_hip`\
`bone_id_right_knee`\
`bone_id_right_foot`



`marvel_rivals.get_world()`

Returns `uintptr_t` of `UWorld`



`marvel_rivals.get_game_instance()`

Returns `uintptr_t` of `UGameInstance`



`marvel_rivals.get_game_state()`

Returns `uintptr_t` of `AGameStateBase`



`marvel_rivals.world_to_screen(x, y, z)`

Converts world coordinates to screen space\
Returns: `x, y`



`marvel_rivals.get_bone_position(skeletal_mesh, bone_id)`

Returns the world position of the specified bone in the form:\
`x, y, z`



```
-- Utility: logs pointers, ints, or nils cleanly
local function log_ptr(name, value)
    if value == nil or value == 0 then
        engine.log(name .. " = nil or 0", 255, 0, 0, 255)
    else
        engine.log(name .. " = 0x" .. string.format("%X", value), 0, 255, 0, 255)
    end
end
-- Test get_local_player
local local_player = marvel_rivals.get_local_player()
if not local_player then
    engine.log("Local player not available", 255, 0, 0, 255)
else
    engine.log("== Local Player ==", 0, 255, 255, 255)
    for k, v in pairs(local_player) do
        engine.log(k .. " = " .. tostring(v), 200, 200, 200, 255)
    end
end
-- Test get_player_list
local players = marvel_rivals.get_player_list()
if not players then
    engine.log("Player list unavailable", 255, 0, 0, 255)
else
    engine.log("== Player List ==", 255, 255, 0, 255)
    for i, player in pairs(players) do
        engine.log("Player " .. i, 0, 255, 0, 255)
        for k, v in pairs(player) do
            engine.log("  " .. k .. " = " .. tostring(v), 180, 180, 180, 255)
        end
    end
end
-- Test world_to_screen
local sx, sy = marvel_rivals.world_to_screen(0, 0, 0)
engine.log(string.format("world_to_screen(0,0,0) = %.1f, %.1f", sx or 0, sy or 0), 0, 255, 255, 255)
-- Test get_world
log_ptr("marvel_rivals.get_world", marvel_rivals.get_world())
-- Test get_game_instance
log_ptr("marvel_rivals.get_game_instance", marvel_rivals.get_game_instance())
-- Test get_game_state
log_ptr("marvel_rivals.get_game_state", marvel_rivals.get_game_state())
-- Test get_bone_position from local player (if available)
if local_player then
    local mesh = local_player.skeletal_mesh
    local bone_id = local_player.bone_id_head
    if mesh ~= 0 and bone_id then
        local x, y, z = marvel_rivals.get_bone_position(mesh, bone_id)
        engine.log(string.format("bone_position(head) = %.1f, %.1f, %.1f", x, y, z), 0, 200, 255, 255)
    else
        engine.log("Invalid mesh or bone_id_head", 255, 0, 0, 255)
    end
end
```



`marvel_rivals.get_class_dump(pointer)`

**Description**\
Returns a table containing the class fields for the specified class pointer in Marvel Rivals. Each entry in the table includes:\
\- **name** (_string_) – The name of the class field.\
\- **offset** (_integer_) – The memory offset associated with the field.

This is useful for reverse engineering or understanding the internal structure of class objects at runtime.

**Arguments**

**pointer** (_integer_) – The memory address of the class you want to dump.

**Return Type**

<pre><code><strong>{
</strong>    [1] = { name = "PlayerController::AcknowledgedPawn", offset = 0x120 },
    [2] = { name = "Controller::ControlRotation", offset = 0x154 },
    ...
}
</code></pre>

Returns **nil** and logs an error if:\
Argument is missing or not an integer.\
Pointer is null.\
Dump is empty.

**Example Usage**

```
local pointer = 0x1A2B3C4D  -- Replace with actual class pointer (For Example uworld)
local dump = marvel_rivals.get_class_dump(pointer)

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
local pointer = 0x1A2B3C4D  -- Replace with actual class pointer (For Example uworld)
local dump = marvel_rivals.get_class_dump(pointer)

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
