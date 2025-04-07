---
description: Using Networking API
---

# Networking

This example demonstrates how to send an HTTP request and handle network responses in Lua.

```
-- Callback function to handle network responses
function network_callback(response_data,  url)
    fs.write_to_file_from_buffer("dump.txt", response_data)
    engine.log("Received network response: " .. m.read_string(response_data,0), 0, 255, 0, 255)
end

-- Register the network callback
engine.register_on_network_callback(network_callback)

-- Function to send an HTTP request
function send_example_request()
    local url = "https://example.com/api/data"
 
    -- Example headers
    local headers = "MyLuaClient/1.0";

    -- Example POST data
    local post_fields = "param1=value1&param2=value2"

    -- Send the HTTP request
    net.send_request(url, headers, post_fields)
 
    engine.log("Request sent to: " .. url, 255, 255, 255, 255)
end

-- Execute the function to send the request
send_example_request()
```

`engine.register_on_network_callback(callback)`

Registers a function to handle network responses.



`net.send_request(url, headers, post_fields)`

Sends an HTTP request with optional headers and POST data.



**Example Usage:**

1\. The script registers a network callback that logs responses.\
2\. A request is sent to [`https://example.com/api/data`](https://example.com/api/data)\
3\. The request includes headers like `User-Agent` and `Authorization`.\
4\. The request sends POST data with parameters.\
5\. Once the server responds, the callback function logs the response.\


