# Client Documentation

Client uses the SFML graphics library, it's coded in C++.

## How to use it
Use command ```cmake -S . -B Build/``` then ```make -C Build/ -j``` to compile.
Start the client with the command ```./Release/r-type_client```.

## Networking
Client can change IP address and port to connect to the server and the timeout connection time in second. Everything is in the ```client.cfg``` file.

## Functions details

### Components
ActiveBonus : ```ActiveBonus(int ss = ShootStyle::ONEBULLET, int sb = SpeedBoost::SPEEDNORMAL, int fb = ForceBoost::FORCENORMAL)``` allows you to have the type of ball, speed and force.

Animation : ```Animation(int rect)``` sets the top-left position of the texture rectangle.

Audio : ```Audio(float volume, const std::string &path, bool loop)``` sets up the volume, the path to the file and the loop.

Controllable : ```Controllable(const std::string &playerId)``` sets up the player's index, if he has one then the entity is controllable.

Damaging : ```Damaging(int damages)``` sets the damage level of the entity.

Destroyable : ```Destroyable(int hp)``` sets up the number of lives of the entity.

Hitbox : ```Hitbox(int width, int height)``` sets up the length and height of the entity.

MovementPattern : ```MovementPattern(MovementPatterns movementPattern)``` indicates the movement pattern of the entity.

Pickup : ```Pickup(BonusType bonusType = SpeedBoost, bool positive = true)``` indicates whether the entity is takeable.

Position : ```Position(float x = 0, float y = 0)``` set up the position of the entity.

Scale : ```Scale(float scaleX, float scaleY)``` set up the enlargement of the entity.

Text : ```Text(const std::string &text, int size = 1)``` set up the text to display and its size.

Texture : ```Texture(std::string path, int left, int top, int width, int height)``` set up the path to the texture file as well as the information concerning the area to display the texture.

Velocity : ```Velocity(int velocity)``` set up the velocity of the entity.

### Systems
DamageSystem : ```void damageSystem(Registry &r, std::map<size_t, std::pair<sf::Sprite, sf::Texture>> &sprites)``` parse every entity, check if it can take damage, and destroy if damage is higher than life.

PositionDamage : ```positionSystemClient(Registry &r, net::Client &client)``` check if it has any pattern, if not, use keyboard to move entity, otherwise, the entity move automatically.


### main
Reads a configuration file from the current directory.
Then extracts the "host" address and port from this configuration file.
It establishes a network connection with a remote server using this information.
And runs the game, represented by the rtype::Game object, using the network connection.

### mainMenu
It loads the font, the color, the size, and what to write as well as their position.

### MoveUp
Allows you to change the color of the text above when you press the up key and select it.

### MoveDown
Allows you to change the color of the text below when pressing the up key and select it.

### runGame
Register every components needed and create entity with these. Then create a window and check if the page to display is the menu or not.

##updateSprite
Receives all entities, paths and sorts as needed, then updates positions, textures and damage.