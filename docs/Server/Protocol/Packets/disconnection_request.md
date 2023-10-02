# Disconnection request
Type `DISCONNECTION_REQUEST`
```cpp
struct disconnectionRequest
{
    std::uint8_t status;
    std::array<packetTypes, UUID_SIZE> uuid;

    disconnectionRequest(const std::string &cliUuid) : status(REQUEST)
    {
        std::memmove(&uuid, cliUuid.data(), UUID_SIZE);
    }
    disconnectionRequest(uint8_t status) : status(status) {}
};
```
The disconnection packet tells the server the client disconnected from it. No response should be expected from the server and the client must not send anything from now as the server will reject everything unless the client resends a connection request packet.

The client must send its UUID with the packet and the header type must be `DISCONNECTION_REQUEST`