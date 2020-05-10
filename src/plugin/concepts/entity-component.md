# Entity and Component
## What are `Entity` and `Component`
An `Entity` is some unique identifier in the world. The `Entity` has a number of `Components`, these components are nothing more than simple data type. For example a Player entity has Health, Position, and etc. associated, it is also common for entities to have some tag associated that describe the type. In the case of a Player it would be some `Player` struct mark the entity as a Player.


## Example
Let try to define *Player* and *Zombie* as entities in ECS with `Health` and `Position`.

| Player | Zombie | Health | Position      |
|--------|--------|--------|---------------|
| Player |        | 20.0   | 0.0, 0.0, 0.0 |
|        | Zombie | 15.0   | 0.0, 0.0, 0.0 |

Both *Player* and *Zombie* share the components `Health` and `Position` but not the components `Player` and `Zombie` that is used to mark the type of the entity.

We can declare the above components as the following
```rust
// Component used to mark an entity as a player
struct Player;

// Component used to mark an entity as a Zombie
struct Zombie;

// Component storing health
struct Health(f64);

// Component storing position
struct Position {
    x: f64,
    y: f64,
    z: f64,
}
```

Now that we have declared the a few components we can create two entities with the given components and insert it into a world. In a later [chapter on world](./world.md) we will cover insertion in depth and what it actually means.
```rust
use fecs::EntityBuilder;

EntityBuilder::new()
    .with(Player)
    .with(Health(20.0))
    .with(Postion {
        x: 0.0,
        y: 0.0,
        z: 0.0,
    })
    .build()
    .spawn_in(&mut world);

EntityBuilder::new()
    .with(Zombie)
    .with(Health(15.0))
    .with(Position {
        x: 0.0,
        y: 0.0,
        z: 0.0,
    })
    .build()
    .spawn_in(&mut world);
```

By calling `BuiltEntity::spawn` we create two new chunks, in the world, where the entities of the archetypes, `{Player, Health, Position}` and `{Zombie, Health, Position}` are stored. We can add additional components to an entity by calling `World::add`, however this will change the archetype of the entity and we would have to move the entire entity to a new chunk. This is an expensive operation and involves copying all components to a new chunk in heap, it takes `O(n)` and therefor should be avoided if possible, this is the same cost as create an entire new entity. In most cases where you find your self adding and removing some component from an entity a mutable component can be used instead, it has greatly improved performance due to the entity not changing its archetype, it is an `O(1)` operation and is very cheap compared to `World::add`.