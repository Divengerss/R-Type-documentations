# Room Closed

Type `ROOM_CLOSED`
```cpp
struct roomClosed
{
    std::uint64_t roomId;

    roomClosed() : roomId(0UL) {}
    roomClosed(std::uint64_t roomId) : roomId(roomId) {}
};
```

The room closed packet tells the roomId has been closed.
