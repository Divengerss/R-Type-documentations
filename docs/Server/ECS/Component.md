# Component

The Component class is a template, that can be modified to match any requirements.

For example, a Destroyable component could look like this:

```cpp
class Destroyable {
    public:
        Destroyable();
        ~Destroyable();
    private:
        bool _destroyable;
}
```

And a Position component can look like this:
```cpp
class Position {
    public:
        Position();
        ~Position();
    private:
        float _x;
        float _y;
}
```

It is important to understand that the Component class is only used to store values, and should not have any functions.