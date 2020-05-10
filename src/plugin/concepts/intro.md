# Concepts
Feather is quite a bit different from regular Minecraft server software written in Java. Feather is written using the [*Entity Component System*](https://en.wikipedia.org/wiki/Entity_component_system) architecture, which greatly improves the utilization of the CPU, most notable being improved cache hit ratio compared to [*Object Oriented Programming*](https://en.wikipedia.org/wiki/Object-oriented_programming). 

The following definitions is used throughout the book to avoid confusion
1. *Entity* is used to associate data in ECS.
2. *Component* is some data associated with a single *Entity* in ECS.
3. *World* is a container of queryable data associated with *Entity's* in ECS.
4. *Dimension*: Is a world in Minecraft.

Feather uses [Fecs](https://github.com/feather-rs/fecs) which is our own custom ECS built on top of [Legion](https://docs.rs/legion/0.2.1/legion/). We chose Legion as the base of our ECS due to its incredible query performance compared to its alternatives like [Specs](https://docs.rs/specs/0.16.1/specs/). The components that makes up an entity is called its archetype, Legion stores all its entities in chunks based on the archetype. This means that adding or removing components from an entity is an `O(n)` operation and should therefor be avoided. 

Feather is structured with a number of systems running in series, these system may perform their calculations in parallel by utilizing [*Rayon*](https://docs.rs/rayon/1.3.0/rayon/). These systems emit events that effects their outcome, for instance the `block_place_system` system emits both `BlockChangeEvent` and `InteractItemEvent`. The listeners attached to these events may poll in arbitrary data from the world and this is the major reason Systems are run in series and not parallel.

In the following chapters we will cover [*Entity Component System*](https://en.wikipedia.org/wiki/Entity_component_system) and how it is utilized within feather and how you should interact with them. We will also cover the event bus and how we merge tasks into the main Game Loop through the scheduler. 

# Chapters
1. [Entity Component](./entity-component.md)
2. [World](./world.md)
3. [Resource](./resource.md)
4. [System](./system.md)


### Additional resources
1. Theres a great [talk](https://kyren.github.io/2018/09/14/rustconf-talk.html) on ECS from [RustConf 2018](https://2018.rustconf.com/).
2. Theres a great comparison between [Specs](https://docs.rs/specs/0.16.1/specs/) and [Legion](https://docs.rs/legion/0.2.1/legion/) [here](https://csherratt.github.io/blog/posts/specs-and-legion/) by Cora Sherratt who worked on specs.