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
    bool compressed;
    std::size_t compressedSize;
    std::uint64_t roomId;

    packetHeader() : type(PLACEHOLDER), dataSize(0U), compressed(false), compressedSize(0UL), roomId(0UL) {}
    packetHeader(packetTypes type, std::uint16_t dataSize) : type(type), dataSize(dataSize), compressed(false), compressedSize(0UL), roomId(0UL) {}
    packetHeader(packetTypes type, std::uint16_t dataSize, bool compressed, std::size_t compressedSize, std::uint64_t roomId) : type(type), dataSize(dataSize), compressed(compressed), compressedSize(compressedSize), roomId(roomId) {}
};
```

This can be interpreted as the following pseudo-code
```pseudo-code
HEADER
{
    INTEGER type
    16BIT UNSIGNED INTEGER size_of_the_data
    BOOLEAN compressed data
    64BIT UNSIGNED INTEGER size_of_the_compressed_data
    64BIT UNSIGNED INTEGER room id
}
```

The `packetTypes type` refers to the following `Enum`
```cpp
enum packetTypes : std::uint8_t
{
    NONE,
    PLACEHOLDER,
    CONNECTION_REQUEST,
    DISCONNECTION_REQUEST,
    CLIENT_STATUS,
    FORCE_DISCONNECT,
    ECS_VELOCITY,
    ECS_POSITION,
    ECS_HITBOX,
    ECS_CONTROLLABLE,
    KEYBOARD_EVENT,
    ECS_DAMAGES,
    ECS_DESTROYABLE,
    ECS_MOVEMENTPATTERN,
    ECS_SCORE,
    KEEP_CONNECTION,
    CREATE_ROOM,
    ROOM_AVAILABLE,
    ROOM_CLOSED,
    JOINED_ROOM,
    LEFT_ROOM,
    TEXT_MESSAGE,
    ECS_TAG,
    ENTITY_KILLED,
};
```
The `std::uint16_t dataSize` stores an unsigned 16bits integer refering to the packet data size to be read from the recipient. Data must be strictly identical to the data size, if the value if lower than its actual size, it will be truncated, leading to undefined behavior. If the value is greather than its actual size, it will mostly crash or leads to buffer overflow, leading to undefined behavior. If the type is set to `PLACEHOLDER`, no data is expected to be read, setting the `dataSize` to 0.

The `bool compressed` tells the data has been compressed using the ZLIB. The `std::size_t compressedSize` must be set according to the compressed size.
The `std::uint64_t roomId` tells the packet is sent for the room specified only. If set to maximum value of unsigned long, the packet should be read by all clients.

Packet header contains contructors to initialize the header with given values.

Packet lists:

- [Placeholder](Packets/placeholder.md)
- [Connection request](Packets/connection_request.md)
- [Disconnection request](Packets/disconnection_request.md)
- [Client status](Packets/client_status.md)
- [Force disconnect](Packets/force_disconnect.md)
- [ECS Velocity](Packets/ecs_velocity.md)
- [ECS Position](Packets/ecs_position.md)
- [ECS Hitbox](Packets/ecs_hitbox.md)
- [ECS Controllable](Packets/ecs_controllable.md)
- [ECS Damage](Packets/ecs_damage.md)
- [ECS Destroyable](Packets/ecs_destroyable.md)
- [ECS Movement Pattern](Packets/ecs_mouvement_pattern.md)
- [ECS Score](Packets/ecs_score.md)
- [ECS Tag](Packets/ecs_tag.md)
- [Keep Connection](Packets/keep_connection.md)
- [Keyboard Event](Packets/keyboard_event.md)
- [Create Room](Packets/create_room.md)
- [Room Available](Packets/room_available.md)
- [Room closed](Packets/room_closed.md)
- [Joined Room](Packets/joined_room.md)
- [Left Room](Packets/left_room.md)
- [Text Message](Packets/text_message.md)
- [Entity killed](Packets/entity_killed.md)