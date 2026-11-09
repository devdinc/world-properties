# World Properties

Load selected values from each world's `world.properties` file and apply them to Bukkit worlds when Skript loads.

## Requirements

- Skript 2.15+
- skript-reflect 2.6+
- A Bukkit-based server (the implementation uses Bukkit APIs)

## Installation

```
package install https://github.com/devdinc/world-properties
```

## Supported properties

The loader reads non-empty, non-comment lines in `key=value` format.

| Key | Meaning | Example |
|---|---|---|
| `border_center` | World border center X and Z coordinates | `border_center=100,200` |
| `border_size` | World border diameter | `border_size=500` |
| Other keys | Treated as gamerule names | `doDaylightCycle=false` |

Boolean gamerule values (`true` or `false`) are parsed as booleans; other gamerule values are parsed as integers. Border center and border size values are parsed as numbers.

## Example file

For a world named `survival`, place the file at `survival/world.properties` inside the server's world container:

```properties
# World border
border_center=100,200
border_size=500

# Gamerules
doDaylightCycle=false
keepInventory=true
randomTickSpeed=3
```

On load, the script scans world-container directories containing a `level.dat` file, reads their `world.properties`, and applies loaded gamerules and border settings to loaded worlds after one tick.

## Manual loading

The package also exposes:

```skript
load_world_properties_from_folder("survival")
```

This reads the named world's `world.properties` file and stores the parsed settings. The file is expected at `<world-container>/<folder>/world.properties`.

## Notes

- Missing `world.properties` files are ignored.
- Blank lines and lines beginning with `#` are ignored.
- This package uses Bukkit APIs and is not intended for Minestom.

## Source

- Implementation: `src/world-properties.sk`
- Tests: `-tests/`
