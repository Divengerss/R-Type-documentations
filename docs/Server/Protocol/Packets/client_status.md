# Client status

Type `CLIENT_STATUS`
```cpp
struct clientStatus
{
    std::uint8_t status;
    std::array<std::uint8_t, uuidSize> uuid;

    clientStatus() : status(LOSE_CLIENT) {}
    clientStatus(const std::string &cliUuid) : status(LOSE_CLIENT)
    {
        std::memmove(&uuid, cliUuid.data(), uuidSize);
    }
    clientStatus(const std::string &cliUuid, std::uint8_t status) : status(status)
    {
        std::memmove(&uuid, cliUuid.data(), uuidSize);
    }
};
```
The client status packet tells the connected client another one connected or disconnected from the server. If a client disconnects, the status is set to LOSE_CLIENT telling all connected clients that the UUID client disconnected. If a client connected to server, the status is set to NEW_CLIENT.

The client must listen at any time for this type of packet to handle their game properly.