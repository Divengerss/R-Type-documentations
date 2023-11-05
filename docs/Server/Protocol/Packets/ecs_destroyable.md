# ECS Destroyable

Type `ECS_DESTOYABLE`

The ECS destroyable packet tells the received data corresponds to ECS Destroyable components.

The data stored in the memory is as followed:

|          | **0x00** | **0x04** | **0x08** | **0x0C** |
|:--------:|:--------:|:--------:|:--------:|:--------:|
| **0x00** | XXYYYYZZ | AAAAAAAA | AAAAAAAA | BBBBBBBB |
| **0x10** | BBBBBBBB | CCDDDDDD | DDCCDDDD |  DDDDCC  |
| **0x20** | CCCCCCCC |          |          |          |

Note: The CC correspond to the boolean IsNull, meaning that the component doesn't contains any value at this index. If CC is false, then the following memory offset correspond to the component values. The size of component corresponds to the size of the followed memory block.


Packet Header:

- XX: Packet type
- YY: dataSize
- ZZ: compressed
- AA: compressed size
- BB: Room ID

Sparse Array:

- CC: IsNull
- DD: Component data