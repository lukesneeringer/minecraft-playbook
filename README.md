## Minecraft Playbook

This playbook installs Java and [EMSM][1] (and, through it, Minecraft) on
a Unix server. It also configures zero or more worlds on the server, and is
able to install some mods (in particular, Forge-based mods).


### Accepting EULAs

Both Java and Minecraft require accepting EULAs in order to run the software.
These playbooks do so automatically, but require you to explicitly opt in
to this behavior.

Do so by setting the following as host variables:

```yaml
accept_java_eula: yes
accept_minecraft_eula: yes
```


### Defining Worlds

Worlds are defined using the `worlds` variable, defined as a list.
Each item in the list defines a world name (`name`), a version of the
Minecraft server (`server`), and optionally a list of mods to install
(`mods`) and players to have op on the server (`ops`).

All world properties are set to the Minecraft defaults, and may be overridden
individually by passing them to `properties` within each world.

A complete sample world definition looks like this:

```yaml
worlds:
  - name: A Minecraft World
    server: minecraft forge 1.8
    mods:
      - 'http://files.minecraftforge.net/maven/com/github/glitchfiend/biomesoplenty/BiomesOPlenty/1.8-3.0.0.1165/BiomesOPlenty-1.8-3.0.0.1165-universal.jar'
      - 'http://marglyph.s3.amazonaws.com/TooManyItems2015_02_14_1.8_Forge.jar'
    ops:
      - uuid: 2f6a0860-1815-4dd1-817b-789c47bdb7ba
        name: lukesneeringer
        level: 4
    properties:
      level_type: BIOMESOP
      pvp: 'false'
      server_port: 25565
```

Notes:

  * Server versions are defined by EMSM; check its documentation.
    Generally it should either be `vanilla x.y` or `minecraft forge x.y`, in
    lower-case.
  * Ops must be defined including the `uuid`, `name`, and `level`.
    You can [look up a player's UUID][2] if you need to.
  * It is best to always explicitly define the `server_port`.
  * If you need to pass a boolean value to any property, make sure you do
    so as a string (as done in the example above).


### License

All code provided here is considered to be licensed as New BSD
(see the `LICENSE` file).

The software that this playbook installs is licensed under their
own terms; using this does not alter that.


  [1]: http://emsm.readthedocs.org/en/latest/
  [2]: http://mcuuid.net/
