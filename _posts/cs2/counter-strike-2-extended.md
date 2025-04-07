---
description: Counter-Strike 2 - Extended API (cs2)​
---

# Counter Strike 2 - Extended

`trace.cast(startx, starty, startz, endx, endy, endz)`

returns true if endpoint is hit/visible



`cs2.get_interface(module_name, interface_name)`

returns integer/pointer



`cs2.get_cvar(cvar_name)`

returns integer/pointer



`cs2.get_entity_list()`

returns integer/pointer



`cs2.get_entity_system()`

returns integer/pointer



`cs2.get_highest_entity_index()`

returns integer



`cs2.get_global_vars()`

returns integer/pointer



`cs2.get_game_rules()`

returns integer/pointer



`cs2.get_planted_c4()`

returns integer/pointer



`cs2.get_view_matrix()`

returns integer/pointer



`cs2.world_to_screen(x, y, z)`

returns x, y screen coords



`cs2.get_bone_position(bone_array, boneid)`

returns x,y,z world coords



`cs2.get_player_list()`

returns entity list table with `controller`, `pawn`, `clipping_weapon`, `bone_array` as integers/pointers and `is_teammate` as boolean

```
local players = cs2.get_player_list()

if players == nil then
    engine.log("No player list found.", 255, 0, 0, 255)
    return
end

for index, player in pairs(players) do
    engine.log("Player " .. index, 255, 255, 0, 255)
    engine.log("  controller = " .. tostring(player.controller), 200, 200, 200, 255)
    engine.log("  pawn = " .. tostring(player.pawn), 200, 200, 200, 255)
    engine.log("  clipping_weapon = " .. tostring(player.clipping_weapon), 200, 200, 200, 255)
    engine.log("  bone_array = " .. tostring(player.bone_array), 200, 200, 200, 255)
end
```



`cs2.get_local_player()`

returns `controller`, `pawn`, `clipping_weapon`, `bone_array` as integers/pointers for local player

```
local local_player = cs2.get_local_player()

if local_player == nil then
    engine.log("Local player not available.", 255, 0, 0, 255)
    return
end

engine.log("Local Player Info", 0, 255, 0, 255)
engine.log("  controller = " .. tostring(local_player.controller), 200, 200, 200, 255)
engine.log("  pawn = " .. tostring(local_player.pawn), 200, 200, 200, 255)
engine.log("  clipping_weapon = " .. tostring(local_player.clipping_weapon), 200, 200, 200, 255)
engine.log("  bone_array = " .. tostring(local_player.bone_array), 200, 200, 200, 255)
```



`cs2.get_schema_dump()`

**Description**\
Returns a table containing the dumped schema fields for Counter-Strike 2. Each entry in the table includes:\
**name** (_string_) – The schema field name.\
**offset** (_integer_) – The memory offset associated with the field.

**Return Type**

```
{
    [1] = { name = "CCSPlayer_MovementServices::m_bInStuckTest", offset = 0x25A },
    [2] = { name = "CCSPlayer_MovementServices::m_flStuckCheckTime", offset = 0x268},
    [3] = { name = "CCSPlayer_MovementServices::m_nTraceCount", offset = 0x468},
    ...
}
```

If no schema dump is available (e.g., the process is not attached), the function returns nil.



**Example Usage**

```
local dump = cs2.get_schema_dump()

if dump == nil then
    engine.log("Schema dump not available.", 255, 0, 0, 255)
    return
end

for i, entry in ipairs(dump) do
    engine.log(string.format("%s = 0x%X", entry.name, entry.offset), 0, 255, 0, 255)
end
```



**File Dump Example**

```
local dump = cs2.get_schema_dump()

if dump == nil then
    engine.log("No schema dump available or process not attached.", 255, 0, 0, 255)
    return
end

local lines = {}

for i, entry in ipairs(dump) do
    table.insert(lines, string.format("%s = 0x%X", entry.name, entry.offset))
end

local text = table.concat(lines, "\n")

fs.write_to_file("offset_dump.txt", text)
engine.log("Offset dump written to offset_dump.txt", 0, 255, 0, 255)
```
