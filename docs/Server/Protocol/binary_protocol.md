Communication between the server and the players/clients is done using binary packets.

A packet on its own contains a header and its data to transmit.
The header contains the type of packet sent and the size of the following data.
By default (if unchanged in the code) the packet size locally is limited to 1024 bytes.

Here is the packet header structure defined in the Packet.hpp
```cpp
struct packetHeader
{
    packetTypes type;
    std::uint16_t dataSize;

    packetHeader() : type(PLACEHOLDER), dataSize(0) {}
    packetHeader(packetTypes type, std::uint16_t dataSize) : type(type), dataSize(dataSize) {}
};
```

This can be interpreted as the following pseudo-code
```pseudo-code
HEADER
{
    INTEGER type
    16BIT UNSIGNED INTEGER size_of_the_data
}
```

The `packetTypes type` refers to the following `Enum`
```cpp
enum packetTypes
{
    PLACEHOLDER,
    CONNECTION_REQUEST,
    DISCONNECTION_REQUEST,
};
```
The `std::uint16_t dataSize` stores an unsigned 16bits integer refering to the packet data size to be read from the recipient. Data must be strictly identical to the data size, if the value if lower than its actual size, it will be truncated, leading to undefined behavior. If the value is greather than its actual size, it will mostly crash or leads to buffer overflow, leading to undefined behavior. If the type is set to `PLACEHOLDER`, no data is expected to be read, setting the `dataSize` to 0.

Packet header contains contructors to initialize the header with given values.

Packet lists:

- [Connection request]()
- [Disconnection request]()