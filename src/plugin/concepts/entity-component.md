# Entity and Component
## What are `Entity` and `Component`
An `Entity` is some unique identifier in the world. The `Entity` has a number of `Components`, these components are nothing more than simple data type. For example a Player entity has Health, Position, and etc. associated, it is also common for entities to have some tag associated that describe the type. In the case of a Player it would be some `Player` struct identifying the entity as a Player.


## Example
Let try to define *Player* and *Zombie* as entities in ECS with `Health` and `Postion`.

| Player | Zombie | Health | Position      |
|--------|--------|--------|---------------|
| Player |        | 20.0   | 0.0, 0.0, 0.0 |
|        | Zombie | 15.0   | 0.0, 0.0, 0.0 |

Both *Player* and *Zombie* share the components `Health` and `Postion` but not the components `Player` and `Zombie` that is used to uniquely identify the type of the entity.

We can declare the above components as the following
```rust
#extern crate legion;
#use legion::prelude::*;

// Component used to identify an entity as a player
struct Player;

// Component used to identify an entity as a Zombie
struct Zombie;

// Component storing health
struct Health(f64);

// Component storing postion
struct Postion {
    x: f64,
    y: f64,
    z: f64,
}
#
#fn main() {
#    let universe = Universe::new();
#    let mut world = universe.create_world();
#
#    world.insert(
#        (),
#        std::iter::once((
#            Player, Health(20.0), 
#            Postion { 
#                x: 0.0, 
#                y: 0.0, 
#                z: 0.0 
#            }
#        ))
#    );
#
#    world.insert(
#        (),
#        std::iter::once((
#            Zombie, 
#            Health(20.0), 
#            Postion { 
#                x: 0.0, 
#                y: 0.0, 
#                z: 0.0 
#            }
#        ))
#    );
#}
```