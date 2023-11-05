# Create room

Type `CREATE_ROOM`
```cpp
struct createRoom
{
    std::uint64_t roomId;
    std::uint8_t maxSlots;

    createRoom(std::uint8_t maxSlots) : roomId(0UL), maxSlots(maxSlots) {}
    createRoom(std::uint64_t roomId, std::uint8_t maxSlots) : roomId(roomId), maxSlots(maxSlots) {}
};
```
The creat room packet asks the server if the client can create a room. The client is expected to provide the maximum slots of player for the room. The Server will respond with the room identifier set in the roomId.
