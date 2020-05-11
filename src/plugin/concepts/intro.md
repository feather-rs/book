# Concepts
Feather is quite a bit different from regular Minecraft server software written in Java. Feather is written using the [*Entity Component System*](https://en.wikipedia.org/wiki/Entity_component_system) architecture, which greatly improves the utilization of the CPU, most notable being improved cache hit ratio, compared to [*Object Oriented Programming*](https://en.wikipedia.org/wiki/Object-oriented_programming).

The following definitions is used throughout the book to avoid confusion
1. *[Entity](TODO)* is a unique identifier used to associate data in ECS.
2. *[Component](TODO)* is a container of data associated with a single *entity* in ECS.
3. *[World](TODO)* is a container of queryable data associated with *entity's* in ECS.
4. *[Spawn](TODO)* is the action of inserting an entity and its components into a world in ECS.
5. *[Despawn](TODO)* is the action of removing an entity and its components from a world in ECS.
6. *[Dimension](TODO)* is a world in Minecraft.

## Chapters
1. [Entity Component](./entity-component.md)
2. [World](./world.md)
3. [Resource](./resource.md)
4. [System](./system.md)
5. [Scheduler](./scheduler.md)
6. [Events](./events.md)


### Additional resources
1. Theres a great [talk](https://kyren.github.io/2018/09/14/rustconf-talk.html) on ECS from [RustConf 2018](https://2018.rustconf.com/).
2. Theres a great comparison between [Specs](https://docs.rs/specs/0.16.1/specs/) and [Legion](https://docs.rs/legion/0.2.1/legion/) [here](https://csherratt.github.io/blog/posts/specs-and-legion/) by Cora Sherratt who worked on specs.