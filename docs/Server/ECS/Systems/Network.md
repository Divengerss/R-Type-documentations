# NetworkSystem

The network system provided a way to communicate with the server and modify the ECS content upon receiving a packet.

It is accessible inside the NetworkSystem.hpp file

Here are the function definitions

## Constructors / Destructors
### NetworkSystem
`NetworkSystem()`

Ctor of the system.

### ~NetworkSystem
`~NetworkSystem()`

Dtor of the system.

### newPlayer
`std::pair<float, float> newPlayer(std::uint64_t roomId, Registry &ecs, const std::string &clientUUID)`

Adds the new player UUID into the registry of the room identifier.

### removePlayer
`void removePlayer(Registry &ecs, const std::string &clientUUID)`

Remove the player UUID from the registry provided.

### affectControllable
`void affectControllable(Registry &ecs, const std::string &clientUUID, int keyCode)`

Handles the received input from the client UUID inside the given ecs.

### addClientToRoom
`bool addClientToRoom(const std::string &clientUUID, std::uint64_t roomId)`

Adds the new client UUID to the given room identifier.

### removeClientFromRoom
`bool removeClientFromRoom(const std::string &clientUUID, std::uint64_t roomId)`

Removes the given client UUID from the roomId.

### roomExist
`bool roomExist(std::uint64_t roomId)`

Check if the given room identifier exists. Returns true if so or false.

### createNewRoom
`std::uint64_t createNewRoom(std::uint8_t maxSlots)`

Creates a new room with the given maximum number of player allowed.

### deleteRoom
`void deleteRoom(std::uint64_t roomId)`

Deletes the given room from the list.

### sendResponse
`void sendResponse(const packet::packetTypes &type, T &data, std::uint64_t roomId = std::numeric_limits<std::uint64_t>::max(), bool toServerEndpoint = false, const std::string cliUuid = "")`

Asks the network to send a response to the clients of the given room identifier.

### sendSparseArray
`void sendSparseArray(const packet::packetTypes &type, sparse_array<T> &sparseArray, std::uint64_t roomId, const std::string &cliUuid = "")`

Asks the network to send the sparse array to the clients of the given room identifiers.

### isServerAvailable
`bool isServerAvailable()`

Asks the network if the socket is opened.

### getConnectedNb
`std::size_t getConnectedNb(std::uint64_t roomId)`

Returns the number of clients connected to the given room identifier.

### getRooms
`std::vector<Room> &getRooms() noexcept`

Returns the vector of rooms already created.

### initRoom
`void initRoom(std::uint64_t roomId, std::unordered_map<std::uint64_t, Registry> &regs)`

Initialize the ECS for the newly created room. This is mandatory before doing anything with the registry.

## Handlers
### handleTextMessage
`void handleTextMessage(const std::array<std::uint8_t, packetSize> &packet, const packet::packetHeader &header)`

Reads the received packet message and sends it back to all clients in the room.

### handleConnectionRequest
`void handleConnectionRequest(std::unordered_map<std::uint64_t, Registry> &regs, packet::packetTypes type, std::array<std::uint8_t, packetSize> &packet)`

Reads the received packet connection request and performs the required actions to satisfy the client needs. The connection can be rejected if the information asked are corrupted or invalid.

### handleDisconnectionRequest
`void handleDisconnectionRequest(std::unordered_map<std::uint64_t, Registry> &regs, const std::array<std::uint8_t, packetSize> &packet, const packet::packetHeader &header)`

Reads the received packet disconnection request and performs the required actions to disconnect the client.

### handleEntityKilled
`void handleEntityKilled(Entity entity, std::uint64_t roomId)`

Sends a packet to all clients in the given room identifier that the given entity has been killed.

### handleKeyboardEvent
`void handlekeyboardEvent(std::unordered_map<std::uint64_t, Registry> &regs, const std::array<std::uint8_t, packetSize> &packet, const packet::packetHeader &header)`

Calls the affectControllable function to handle the keyboard events.

### handleCreateRoom
`void handleCreateRoom(std::unordered_map<std::uint64_t, Registry> &regs, const std::array<std::uint8_t, packetSize> &packet)`

Reads the received packet to create a new room.

### handleKeepConnection
`void handleKeepConnection(const std::array<std::uint8_t, packetSize> &packet, const packet::packetHeader &header)`

Accept the client response to the connection ping.

## Miscellaneous
### networkSystemServer
`void networkSystemServer(std::unordered_map<std::uint64_t, Registry> &regs)`

The core function of the networkSystemServer

### getClients
`std::vector<net::Client> &getClients() noexcept`

Asks the network to return the client list as a vector of Client class.

### removeClient
`void removeClient(const std::string &clientUUID)`

Asks the network to removes the given client UUID from the list.

### writeToLogs
`void writeToLogs(const std::string_view &status, const std::string &msg)`

Asks the network to write to the server log the provided message.

### removeTimeoutClients
`bool removeTimeoutClients(std::uint64_t roomId, Registry &ecs)`

Removes the no longer connected or too slow clients from the given room identifier.