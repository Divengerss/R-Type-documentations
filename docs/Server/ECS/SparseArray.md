# SparseArray

The SparseArray is a vector of optional [Components](Component.md).

For example, a SparseArray named 'Velocity' will be able to store the velocity of each [Entity](Entity.md).
If an [Entity](Entity.md), for example a wall, doens't need a Velocity component, than the value for this [Entity](Entity.md) in the Velocity SparceArray will be empty, hence the "optional Component".



The class SparseArray looks like this:

```cpp
class sparse_array
{
public:
    using value_type = std::optional<Component>;
    using reference_type = value_type &;
    using const_reference_type = value_type const &;
    using container_t = std::vector<value_type>;
    using size_type = typename container_t::size_type;
    using iterator = typename container_t::iterator;
    using const_iterator = typename container_t ::const_iterator;

    sparse_array() {};
    sparse_array(const sparse_array &other);
    sparse_array(sparse_array &&other) noexcept;
    ~sparse_array();

    sparse_array &operator=(const sparse_array &other);
    sparse_array &operator=(sparse_array &&other) noexcept;
    reference_type operator[](size_t idx);
    const_reference_type operator[](size_t idx) const;

    iterator begin();
    const_iterator begin() const;
    const_iterator cbegin() const;
    iterator end();
    const_iterator end() const;
    const_iterator cend() const;
    size_type size() const;

    reference_type insert_at(size_type pos, Component const &value);
    reference_type insert_at(size_type pos, Component &&value);
    template <class... Params>
    reference_type emplace_at(size_type pos, Params &&...data);
    reference_type push_back(std::optional<Component> &&value);
    void erase(size_type pos);
    size_type get_index(value_type const &value) const;

private:
    container_t _data;
};
```


## Constructors/Destructor
### sparse_array()
```cpp
sparse_array() {};
```
The default constructor of the SparseArray class.

### sparse_array(const sparse_array)
```cpp
sparse_array(const sparse_array &other);
```
The copy constructor of the SparseArray class.

### sparse_arrray(sparse_array &&)
```cpp
sparse_array(sparse_array &&other) noexcept;
```
The move constructor of the SparseArray class.

### ~sparse_array()
```cpp
~sparse_array();
```
The default destructor of the SparseArray class.

## Operators
### &operator=
```cpp
sparse_array &operator=(const sparse_array &other);
```
The copy assignment operator of the SparseArray class.

### &operator=
```cpp
sparse_array &operator=(sparse_array &&other) noexcept;
```
The move assignment operator of the SparseArray class.

### &operator[]
```cpp
reference_type operator[](size_t idx);
```
Takes the index of a [Entity](Entity.md) and returns a reference to the value contained in the array for this entity.

### &operator[]
```cpp
const_reference_type operator[](size_t idx) const;
```
Same but returns a const reference instead of a reference.

## Functions
### insert_at()
```cpp
reference_type insert_at(size_type pos, Component const &value);
```
Inserts the value at the specified position, and returns the reference to the value.

### insert_at()
```cpp
reference_type insert_at(size_type pos, Component &&value);
```
Same but moves the value instead of copying it.

### emplace_at()
```cpp
template <class... Params>
reference_type emplace_at(size_type pos, Params &&...data);
```
Same as `insert_at` but moves the value instead of copying it.

### push_back()
```cpp
reference_type push_back(std::optional<Component> &&value);
```
Insert the value at the back of the array, and returns a reference to the value.

### erase()
```cpp
void erase(size_type pos);
```
Erases the value at the specified position.

### get_index()
```cpp
size_type get_index(value_type const &value) const;
```
Take a reference to an optional [Component](Component.md), and return its index.
Allows us to retreive the index of an [Entity](Entity.md) its value.

## Value
### _data
```cpp
container_t _data
```
Vector of optional [Components](Component.md)