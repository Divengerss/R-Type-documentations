# Joined Room

Type `JOINED_ROOM`
```cpp
struct joinedRoom
{
    std::array<std::uint8_t, uuidSize> uuid;
    std::uint64_t roomId;

    joinedRoom() : uuid({}), roomId(0UL) {}
    joinedRoom(const std::string &clientUUID, std::uint64_t roomId) : roomId(roomId)
    {
        std::memmove(&uuid, clientUUID.data(), uuidSize);
    }
};
```

The joined room packet tells the client UUID joined the room ID.
