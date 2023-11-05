# Connection request

Type `CONNECTION_REQUEST`
```cpp
struct connectionRequest
{
    std::uint8_t status;
    std::array<std::uint8_t, UUID_SIZE> uuid;

    connectionRequest() : status(REQUEST)
    {
        std::memset(&uuid, 0, UUID_SIZE);
    }
    connectionRequest(uint8_t status, const std::string &cliUuid) : status(status)
    {
        std::memmove(&uuid, cliUuid.data(), UUID_SIZE);
    }
};
```
The connection request packet asks the server if the client can connect to the server. The client is not expected to provide anything upon sending the packet, however, the packet type must be revelant in the header.

The `std::uint8_t status` refers to the server response and so, doesn't need to be set from the client. The server will response with `ACCEPTED` anyway, as the connection will always be valid, even if the client is already connected to the server. It is the client job to check if he already has an open connection with the server.

When receiving the packet response from the server, the `dataSize` should be set to `UUID_SIZE`, or 37 bits (is unchanged in the code) containing the UUID the client holds on the server. This Universally Unique Identifier must be used from now to send any packets to the server, if no UUID are provided, the server will refuse them.

The UUID represent a string as follow:
`XXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX`