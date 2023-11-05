# Keyboard Event

Type `KEYBOARD_EVENT`
```cpp
struct keyboardEvent
{
    std::uint8_t _status;
    std::array<std::uint8_t, uuidSize> uuid;
    int keyCode;
    std::uint64_t roomId;

    keyboardEvent() : _status(0), keyCode(-1), roomId(0UL) {};
    keyboardEvent(const std::string &cliUuid, std::uint8_t status, int key, std::uint64_t roomId) : _status(status), keyCode(key), roomId(roomId)
    {
        std::memmove(&uuid, cliUuid.data(), uuidSize);
    };
};
```

The keyboard event packet handles the given input keyCode by the client UUID from the roomId. The status specify if the asked input has been accepted or not.