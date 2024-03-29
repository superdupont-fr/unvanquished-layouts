This repo contains various layouts to be used by unvanquished
server hosts.

The "default.dat" layouts are here to allow random selection
in maprotations.cfg but are simply the builtin layouts
extracted from their original map.

== File organisation ==

All layouts are in `./layouts/$MAP/` folder.
By convention, files are named as such:

* `default.dat` for the layout extracted from the original
	map;
* `alt${NUM}.dat` to provide alternative layouts for regular
	games, that is, PvP, where ${NUM} is a unique number;
* `${SPECIES}pve${NUM}.dat` to provide "mission-style"
	layouts, that is, one team should not be played by real
	players. ${NUM} is a unique number;
* `${SPECIES}pve${NUM}.txt` to provide rules for PvE layouts;

This repo also includes basic navmesh connection files
required to help bots navigating.
Those files are named as: "maps/${MAP}-${CLASS}.navcon", where
${CLASS} must be one of:

* human_bsuit
* human_naked
* level0
* level1
* level2
* level2upg
* level3
* level3upg
* level4

Granger navmeshes are intentionally skipped since bots are
not yet able to choose this class.
The navmesh files should not be considered reliable.

== Creating layouts ==

Here is a small list of useful commands (you need to spawn
the console to use them) to create a layout, as there is
currently no easy to use GUI to help with that:

* `/devmap ${MAP}` starts a game with ${MAP}, enabling
	cheating. Cheating is required to save a layout;
	It is possible to load an existing layout by appending
	said layout's name, that is: `/devmap ${MAP} ${LAYOUT}`;
* `g_instantBuilding 1`: this removes the need to wait when
	you buid or removes something. It also allows to remove
	the last spawn and unique buildings (RC/OM). Doing this
	might make the game end, though!
* `g_neverEnd 1` prevent the game to end if a team have no
	spawns and no players;
* `/noclip` allows you to no longer be affected by geometry.
	This is pretty useful as human, but with noclip enabled,
	you won't be able to wallwalk and hence to put alien
	buildings on walls and ceilings;
* `/devteam [a|h]` makes you either a naked human with CKit
	or an advanced granger, where you currently are, switching
	team if necessary;
* `layoutSave ${LAYOUT}` saves the layout in your unvanquished
	local folder, under `./game/layouts/${MAP}/${LAYOUT}.dat`;
* `layoutLoad ${LAYOUT}` reloads the map with ${LAYOUT};
* `cg_drawBBox 1` allows you to see the collision boxes of
	buildings, useful to make sure something can or not be hit,
	or to ensure a barricade really blocks a door;
* `/god` prevents you from taking any damage;
* `give bp` gives your team a lot of build points. Specific
	number can be provided to add more (or remove if negative).
	Keep in mind that the starting number of BPs is not set by
	layout, but by server and map configurations, and hence you
	might end up with disabled buildings in real games!
* `give momentum` gives your team the maximum momentum. As for
	`give bp`, you can specify the amount, which can be
        negative;
* `listlayouts` when in game will list all available layouts
	for current map;

Keep in mind that several of those changes will stay around
in normal (`/map $MAP`) local games!
Notably, g_instantBuilding will.

== Enabling layouts in map rotations ==

Example of `maprotation.cfg` entry to use random layout:

```
station15 {
	layouts "default" "alt1"
}
```

Note that it is currently not possible to automatically load
a specific configuration file depending on the layout, so
mission-style layouts must be setup manually.

== Navmesh improvements ==

For some PvE layouts, bots needs additional connections to
travel correctly and give a decent challenge. Those are
placed in the "map" folder.
