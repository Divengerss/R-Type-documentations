# How to use the ECS

This ECS can be used for any purpose, like creating video games, or mobile applications, ect.

A basic implementation would be:
``` cpp
    int main() {
        Registry reg;
        reg.register_component<Position>();
        Entity e = reg.spawn_entity();
        Position pos = {1, 2};
        reg.add_component<Position>{pos, e};
    }
```

I will explain line per line how this works:

```
Registry reg;
```
Here we create a new Registry object.

```
reg.register_component<Position>();
```
We register the Position component in the registry, so that we can add a Position component to our future entities.

```
Entity e = reg.spawn_entity();
```
We create a new Entity, made by the Registry, and is also added to every SparseArray already created.

```
Position pos = {1, 2};
```
We create a Position component.

```
reg.add_component<Position>{pos, e};
```
We set the Position component we created earlier to the Entity.


The position of the Entity can now be retrieved using:
```reg.get_components<Position>()[e()];```
