# Keep Connection

Type `KEEP_CONNECTION`
```cpp
struct keepConnection
{
    std::array<std::uint8_t, uuidSize> uuid;

    keepConnection()
    {
        std::memset(&uuid, 0, uuidSize);
    }
    keepConnection(const std::string &clientUUID)
    {
        std::memmove(&uuid, clientUUID.data(), uuidSize);
    }
};
```

This packet is sent by the server to the client of UUID to keep track of their connection. If the client doesn't respond after N number of packets of this type sent, the client is disconnected from the server.