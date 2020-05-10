# Concepts
Feather is quite a bit different from regular Minecraft server software written in Java. Feather is written using the [*Entity Component System*](https://en.wikipedia.org/wiki/Entity_component_system) method, which greatly improves the utilization of the CPU, most notable being improved cache hit ratio compared to [*Object Oriented Programming*](https://en.wikipedia.org/wiki/Object-oriented_programming). 

Definitions of words that are shared with Minecraft but has nothing to do with Minecraft.
1. *Entity* is a unique identifier.
2. *Component* is some data associated with an *Entity*.
3. *World* is a container of queryable data associated with *Entity's*.

Feather is structured with a number of systems running in series, these system may perform their calculations in parallel by utilizing [*Rayon*](https://docs.rs/rayon/1.3.0/rayon/). These systems emit events that effects their outcome, for instance the `block_place_system` system emits both `BlockChangeEvent` and `InteractItemEvent`. The listeners attached to these events may poll in arbitrary data from the world and this is the major reason Systems are run in series and not parallel.

In the following chapters we will cover [*Entity Component System*](https://en.wikipedia.org/wiki/Entity_component_system) and how it is utilized within feather and how you should interact with them. We will also cover the event bus and how we merge tasks into the main Game Loop through the scheduler. 

# Chapters
1. [Entity Component](./entity-component.md)
2. [Resource](./resource.md)
3. [World](./world.md)
4. [System](./system.md)
