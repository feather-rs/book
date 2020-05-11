# World

When writing plugins for feather you will rarely have to create your own world, since feather provides two worlds that one of which are available asynchronous. But for the purpose of demonstrating ECS will be crating our own world, which is no different from a provided one.

We can create a world in Fecs by simply calling `World::new`.
```rust
use fecs::World;

let world = World::new();
```

The set of components that makes up an entity is called archetype, Legion stores all its entities in chunks based on the archetype. This means that adding or removing components from an entity is an `O(n)` operation and should therefor be avoided. 

By calling `BuiltEntity::spawn` we create two new chunks, in the world, where the entities of the archetypes, `{Player, Health, Position}` and `{Zombie, Health, Position}` are stored. We can add additional components to an entity by calling `World::add`, however this will change the archetype of the entity and we would have to move the entire entity to a new chunk. This is an expensive operation and involves copying all components to a new chunk in heap, it takes `O(n)` and therefor should be avoided if possible, this is the same cost as create an entire new entity. In most cases where you find your self adding and removing some component from an entity a mutable component can be used instead, it has greatly improved performance due to the entity not changing its archetype, it is an `O(1)` operation and is very cheap compared to `World::add`.