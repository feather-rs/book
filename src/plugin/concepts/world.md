# World

When writing plugins for feather you will rarely have to create your own world, since feather provides two worlds that one of which are available asynchronous. But for the purpose of demonstrating ECS will be crating our own world, which is no different from a provided one.

We can create a world in Fecs by simply calling `World::new`.
```rust
use fecs::World;

let world = World::new();
```

