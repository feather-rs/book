# Lieutenant
Lieutenant is Feather's easy to use and powerful command library.
Lets try it out, by first define a provider for the `MessageReceiver` type for convenience.

```rust
struct CommandCtx<'a> {
  source: Entity,
  game: &'a mut Game,
  world: &'a mut World,
}

#[provider]
fn provide_source(ctx: &mut CommandCtx) -> Result<MessageReceiver> {
    ctx.world.try_get::<MessageReceiver>(ctx.source)
        .map_err(Error::Custom("No command source associated with this command call."))
}
```

We can then define the command `[Literal("hello"), Literal("world"]` command which depends on the `MessageReceiver` provider.
```rust
#[command(usage = "hello world")]
fn hello_world(source: &mut MessageReceiver) {
    source.send("hello world" * Color::Green);
}
```

We could also define `hello_world` without relying on the provider, this can be done as such.
```rust
#[command(
    usage = "hello world", 
    description = "sends \"hello world\" to the source of the command"
)]
fn hello_world(ctx: &mut CommandCtx) -> Result<()> {
    let source = ctx.world.try_get::<MessageReceiver>(ctx.source)
        .map_err(Error::Custom("No command source associated with this command call."))
    source.send("hello world" * Color::Gold * Style::Bold);
    Ok(())
}
```

We can also define more complex commands, lets try to define the gamemode command from vanilla Minecraft.

```rust
enum GameMode {
    Survival,
    Creative,
    Adventure,
    Spectator,
}

#[command(usage = "gamemode <gamemode> [target]")]
fn gamemode(
    source_sink: &mut MessageReceiver, 
    source_gamemode: &mut GameMode,
    gamemode: GameMode, 
    target: Option<Target<Player<(&UserName, &mut MessageReceiver, &mut GameMode)>>>
) {
    if let Some((username, target_sink target_gamemode)) = target {
        *target_gamemode = gamemode;
        target_sink.send("Your game mode has been changed")
        source_sink.send("Set {} game mode to {} Mode", target_username, gamemode);
    } else {
        *surce_gamemode = gamemode;
        player.send(format!("Set own game mode to {} Mode", gamemode));
    }
}
```
