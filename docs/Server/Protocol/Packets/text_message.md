# Text Message

Type `TEXT_MESSAGE`
```cpp
struct textMessage
{
    std::array<std::uint8_t, uuidSize> uuid;
    std::array<std::uint8_t, 256UL> message;
    std::size_t msgSize;

    textMessage(): uuid({}), msgSize(0UL)
    {
        std::memset(&message, 0, 256UL);
    }
    textMessage(const std::string &cliUuid, const std::string &msg) : msgSize(msg.length())
    {
        std::memset(&message, 0, 256UL);
        std::memmove(&uuid, cliUuid.data(), uuidSize);
        std::memmove(&message, msg.data(), msgSize);
    }
};
```

The text message packet tells a message has been sent by the client UUID. The maximum size is 256UL. 