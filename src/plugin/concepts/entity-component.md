# What are `Entity` and `Component`
An `Entity` is a unique identifier that usually has a number of `Components` associated, these components are nothing more than simple data containers. For example a Player entity could have the attributes `Health` and `Position` associated. It is also common for entities to have a marker component associated, the marker is used to identify and describe the type of an entity. In the case of a Player it would be a `struct Player;` that is used to mark the entity as a Player.

Modeling a *Player* in ECS starts by defining some components that holds attributes for the player.
```rust,noplaypen
// Component used to mark an entity as a player
struct Player;

// Component storing health
struct Health(f64);

// Component storing position
struct Position {
    x: f64,
    y: f64,
    z: f64,
}
```
Here `Health` and `Postion` attributes could be shared across multiple types of entities, but the player marker would only exist for a Player entity. We could define a separate `Zombie` marker for a Zombie and have it share `Health` and `Postion` components with the Player.
```rust,noplaypen
// Component used to mark an entity as a zombie
struct Zombie;
```
In ECS each entity and its associated components are stored in a world, we can imagine the world being a large matrix where each column is a component, each row a unique entity, and each cell component data associated with the entity.

| Player | Zombie | Health | Position      |
|--------|--------|--------|---------------|
| Player |        | 20.0   | 0.0, 0.0, 0.0 |
|        | Zombie | 15.0   | 0.0, 0.0, 0.0 |


Now that we have defined two marker components `Player` and `Zombie`, and the associated attribute components `Health` and `Postion`, we can create Player and Zombie as entities and spawn them into the ECS world.
```rust,noplaypen
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
