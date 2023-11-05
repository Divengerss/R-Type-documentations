# Room Available

Type `ROOM_AVAILABLE`
```cpp
struct roomAvailable
{
    std::uint64_t roomId;
    std::uint8_t maxSlots;

    roomAvailable() : roomId(0UL), maxSlots(0UL) {}
    roomAvailable(std::uint64_t roomId, std::uint8_t maxSlots) : roomId(roomId), maxSlots(maxSlots) {}
};
```

The room available packet tells a new room has been created with the ID roomId containing the maxium of maxSlots players.
