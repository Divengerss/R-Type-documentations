# Left Room

Type `LEFT_ROOM`
```cpp
struct leftRoom
{
    std::array<std::uint8_t, uuidSize> uuid;
    std::uint64_t roomId;

    leftRoom() : uuid({}), roomId(0UL) {}
    leftRoom(const std::string &clientUUID, std::uint64_t roomId) : roomId(roomId)
    {
        std::memmove(&uuid, clientUUID.data(), uuidSize);
    }
};
```

The left room packet tells the client UUID left the room ID.
