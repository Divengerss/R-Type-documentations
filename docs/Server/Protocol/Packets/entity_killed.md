# Entity killed

Type `ENTITY_KILLED`
```cpp
struct entityKilledStatus
{
    int entity;

    entityKilledStatus(int entity) : entity(entity){};
};
```

The entity killed packet stores the entity index to be killed.
