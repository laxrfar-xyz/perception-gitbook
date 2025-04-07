---
description: Registering and Using Callbacks
---

# Registering Callbacks

This example demonstrates how to register and use engine callbacks in Lua.

<pre><code><strong>-- Callback function for engine tick (executed every tick)
</strong>function enginetick_callback()
    -- Your logic here (executed on every engine tick)
end

-- Callback function for when the script is unloaded
function on_unload_callback()
    engine.log("Script is being unloaded", 255, 255, 255, 255)
end

-- Callback function for network responses
function on_net_callback(str)
    engine.log("Network Response: " .. str, 255, 255, 255, 255)
end

-- Register the callbacks with the engine
engine.register_on_engine_tick(enginetick_callback)
engine.register_onunload(on_unload_callback)
engine.register_on_network_callback(on_net_callback)
</code></pre>



`engine.register_on_engine_tick(callback)`

Registers a function to be executed on every engine tick (1 frame).



`engine.register_onunload(callback)`

Registers a function that is executed when the script is unloaded.



`engine.register_on_network_callback(callback)`

Registers a function to handle network responses.
