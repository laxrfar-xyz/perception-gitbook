---
description: Using the Rendering API
---

# Rendering

This example demonstrates how to use the rendering functions in Lua.

```
-- Create a font for rendering text
local font_handle = render.create_font("Verdana", 25, 400)

-- Get the screen size
local screen_size_x, screen_size_y = render.get_viewport_size()

-- Callback function for rendering
function enginetick_callback()
    -- Draw a white diagonal line
    render.draw_line(500, 500, 600, 600, 255, 255, 255, 255, 5)

    -- Draw a filled yellow rectangle
    render.draw_rectangle(700, 700, 50, 50, 255, 255, 0, 255, 1, true)

    -- Draw a filled red circle
    render.draw_circle(900, 900, 25, 255, 0, 0, 255, 5, true)

    -- Draw text in magenta with a white outline
    render.draw_text(font_handle, "Test", 1000, 1000, 255, 0, 255, 255, 5, 255, 255, 255, 255)

    -- Draw a red triangle
    render.draw_triangle(500, 500,600, 600, 800, 800, 255, 0, 0, 255, 1, false)
end
```

`render.create_font("Verdana", 25, 400)`

Creates a font with the specified name, size, and weight.



`render.get_viewport_size()`

Retrieves the screen size for reference.



`render.draw_line(x1, y1, x2, y2, r, g, b, a, thickness)`

Draws a diagonal line.



`render.draw_rectangle(x, y, width, height, r, g, b, a, thickness, filled)`

Draws a rectangle.



`render.draw_circle(x, y, radius, r, g, b, a, thickness, filled)`

Draws a filled circle.



`render.draw_text(font, text, x, y, r, g, b, a, outline_thickness, o_r, o_g, o_b, o_a)`

Draws text



`render.draw_triangle(x1, y1, x2, y2, x3, y3, r, g, b, a, thickness, filled)`

Draws triangle.



`render.get_fps()`

Gets overlay FPS



`render.create_bitmap_from_url(url)`

Creates a bitmap from a URL.



`render.create_bitmap_from_buffer(buffer_handle)`

Creates a bitmap from buffer handle



`render.create_bitmap_from_file(file_name)`

Creates a bitmap from a file
