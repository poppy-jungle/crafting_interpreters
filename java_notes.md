# Java concepts

### `static`
Used to indicate something belongs to the class itself:
- Static variables: Shared across all instances of the class. They are usually used for constants or class-level data.
- Static methods: Can be called without an instance of the class. They can only access static variables and other static methods.
- Static blocks: Used for initialization of static variables or other setup when the class is loaded.
- Static classes: Inner classes that can exist independently of an outer class instance.

### `final`
Non-access modifier used in:
- Variables to create constant
- Methods to prevent method overloading
- Classes to prevent inheritance