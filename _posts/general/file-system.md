---
description: Using File System API
---

# File System

This example demonstrates how to use the filesystem functions in Lua.

```
-- Check if the file "test.txt" exists
if fs.does_file_exist("test.txt") == true then
    -- Read the file contents
    local read_data = fs.read_from_file("test.txt")

    -- Delete the file after reading
    fs.delete_file("test.txt")

    -- Log the file contents
    engine.log(read_data, 255, 255, 255, 255)
else
    -- Create and write data to the file
    fs.write_to_file("test.txt", "test data")

    -- Log that the file did not exist
    engine.log("File does not exist", 255, 255, 255, 255)
end
```

`fs.does_file_exist(file_name)`

Checks if the file exists.



`fs.read_from_file(file_name)`

Reads data from a file.



`fs.write_to_file(file_name, data)`

Writes data to a file.



`fs.delete_file(file_name)`

Deletes the specified file.



`engine.log(message, r, g, b, a)`

Logs the message to the console with color.



`fs.write_to_file_from_buffer(file_name, buffer_handle)`

Writes all contents of a buffer to a file



`fs.read_from_file_to_buffer(file_name, buffer_handle)`

Reads all file contents into a buffer



`fs.get_file_size(file_name)`

Get the size of a file



**Example Usage:**

If `"test.txt"` exists, the script reads its content, logs it, and deletes the file.\
If `"test.txt"` does not exist, it creates the file and writes `"test data"` to it, then logs that the file was missing.\
Any access outside Documents/My Games is restricted
