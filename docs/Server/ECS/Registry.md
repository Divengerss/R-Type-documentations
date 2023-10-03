# Registry

A Registry is the core class of the ECS, which stores the differents [SparseArrays](SparseArray.md) in an `unordered_map`, using the type of the [Component](Component.md) stored in the [SparseArray](SparseArray.md) as the index in the associative array.

When a [SparseArray](SparseArray.md) is created, it creates multiple functions:
    - a function that allows us to delete the [Component](Component.md) of a given [Entity](Entity.md) (stored in _erase_functions).
    - a function that allows us to add a new [Entity](Entity.md) to the array (stored in _add_functions).

There is also the [Entity](Entity.md) management part in the Registry, to create, delete and update the differents [Components](Component.md) of the [Entity](Entity.md).


The Registry class looks like this:

```cpp
class Registry
{
public:
    Registry(){};

    template <class Component>
    sparse_array<Component> &register_component();

    template <class Component>
    sparse_array<Component> &get_components();

    template <class Component>
    sparse_array<Component> const &get_components() const;

    // #########################################################
    // #                 ENTITY MANAGEMENT                     #
    // #########################################################

    Entity spawn_entity();
    void kill_entity(Entity const &e)

    template <typename Component>
    typename sparse_array<Component>::reference_type add_component(Entity const &to, Component &&c);

    template <typename Component, typename... Params>
    typename sparse_array<Component>::reference_type emplace_component(Entity const &to, Params &&...p);

    template <typename Component>
    void remove_component(Entity const &from);

private:
    std::unordered_map<std::type_index, std::any> _components_arrays;
    std::unordered_map<std::type_index, std::function<void(Registry &, Entity const &)>> _erase_functions;
    std::unordered_map<std::type_index, std::function<void(Registry &)>> _add_functions;
    std::list<int> _empty_entities;
};
```

## Constructor
### Registry()
```cpp
Registry()
```
Default constructor of Registry

## Functions
### register_components()

```cpp
template <class Component>
sparse_array<Component> &register_component();
```
Creates and adds a [SparseArray](SparseArray.md) using the given [Component](Component.md) in the Registry, and returns it.

#### Usage
```cpp
SparseArray velocity = Registry.register_component<Velocity>();
```
Here the Velocity parameter is a [Component](Component.md).

### get_components()
```cpp
template <class Component>
sparse_array<Component> &get_components();
```
Returns the [SparseArray](SparseArray.md) of the given [Component](Component.md).

### get_components()
```cpp
template <class Component>
sparse_array<Component> const &get_components() const;
```
Same but returns a const [SparseArray](SparseArray.md) of the given [Component](Component.md).

# Entity management
## Functions
### spawn_entity()

```cpp
Entity spawn_entity();
```
Creates a new [Entity](Entity.md), by using the index of a previously deleted [Entity](Entity.md) (using `_empty_entities`), or by calling `_add_functions` on every [SparseArray](SparseArray.md) existing, and returns an [Entity](Entity.md) containing the index.

### kill_entity()
```cpp
void kill_entity(Entity const &e);
```
Deletes the [Entity](Entity.md), by calling `_delete_functions` on every [SparseArray](SparseArray.md), and adds the index of the newly deleted [Entity](Entity.md) in `_empty_entities`.

### add_component()
```cpp
template <typename Component>
typename sparse_array<Component>::reference_type add_component(Entity const &to, Component &&c);
```
Adds a value at the given index ([Entity](Entity.md)) to the [SparseArray](SparseArray.md) corresponding to the given [Component](Component.md).

### emplace_component()
```cpp
template <typename Component, typename... Params>
typename sparse_array<Component>::reference_type emplace_component(Entity const &to, Params &&...p);
```
Same, but moves the value instead of copying it.

### remove_component()
```cpp
template <typename Component>
void remove_component(Entity const &from);
```
Removes the value at the given index ([Entity](Entity.md)) from the [SparseArray](SparseArray.md) corresponding to the given [Component](Component.md);

## Values
### _components_arrays
```cpp
std::unordered_map<std::type_index, std::any> _components_arrays;
```
Stores the different [SparseArrays](SparseArray.md).

### _erase_functions
```cpp
std::unordered_map<std::type_index, std::function<void(Registry &, Entity const &)>> _erase_functions;
```
Stores the erase functions created when creating a new [SparseArray](SparseArray.md), using the type of [Component](Component.md) as the index.

### _add_functions
```cpp
std::unordered_map<std::type_index, std::function<void(Registry &)>> _add_functions;
```
Stores the add functions created when creating a new [SparseArray](SparseArray.md), using the type of [Component](Component.md) as the index.

### _empty_entities
```cpp
std::list<int> _empty_entities;
```
Stores the list of empty indexes, used to manage memory cache more efficiently
