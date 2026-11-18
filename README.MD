# DQMJ3P Unobtainable monster synthesis

## General information

This is a RomFS patch that makes all unobtainable monsters of DQMJ3P available through synthesis, so geting these monsters won't requires cheats, plugins, or other out-of-game manipulations (besides installing this patch)

Unlike cheats and plugins, this patch should work regardless of other mods, like translations (as long as these other mods don't change or overwrite files from this patch).

The list of synthesis recipes added by this mod can be found in [SUMMARY.MD](./SUMMARY.MD).

I didn't use any AI, I went and read through a bunch of hex values of the various game files to guess what they mean to make this patch.

### Installation

> In any case, having DQMJ3P and its 1.3 update is required for this patch to work as intended.

- On emulator (Azahar is the recommended one)
  1. Get `DQMJ3PUMS.zip` from the [releases](https://github.com/Enignmeman/DQMJ3P-Unobtainable-monster-synthesis/releases/tag/V0.2)
  2. Unzip it
  3. In the game list, right-click DQMJ3P and choose `Open Mods Location`
  4. Copy the `/romfs/` folder from the extracted archive to the just opened folder window
  5. The patch is installed, you can play the game now :smile:

- On a 3ds with CFW (Luma3DS)

> Don't forget to make sure you have game patching enabled.

  1. Get `DQMJ3PUMS.zip` from the [releases](https://github.com/Enignmeman/DQMJ3P-Unobtainable-monster-synthesis/releases/tag/V0.2)
  2. Unzip it
  3. On your SD card, if they don't exist yet, create a `titles` folder in `/luma/` and a `00040000001ACB00` folder in `/luma/titles/` on your SD card
     - You should have `/luma/titles/00040000001ACB00` now
  4. Copy the `/romfs/` folder from the extracted archive to `/luma/titles/00040000001ACB00`
  5. The patch is installed, you can play the game now :smile:

## Technical information

> All of these files are in little-endian form, so the value `01 00` for example means 1 in decimal and the value `00 01` means 256 in decimal.

### `CouplingCourtRankParam.tp`

This file contains information regarding the synthesis options (or lack of).

Each data block after the 4 bytes-long header is made of 4 bytes:
- 2 bytes for synthesis status
- 2 bytes for monster species ID

Synthesis status can be 4 different values:

|Value|Meaning|
| --- | --- |
|0|Can be acquired through "generic synthesis"|
|1|Can be acquired through "special synthesis"[^1]|
|2|Can be acquired through both "generic synthesis" and "special synthesis"[^2]|
|3|Cannot be acquired through synthesis|

[^1]: Requires a special synthesis recipe to exist, else will act like no synthesis is available.
[^2]: Will act like "generic synthesis" if no special synthesis recipe exists

### `Coupling4Param.tp`

This file contains information regarding the special synthesis recipes.

Each data block after the 4 bytes-long header is made of 6 bytes:
- 2 bytes for the monster species ID of the result
- 2\*2 bytes for each of the 2 monster species IDs of the components to synth together

IDs don't require any particular order.

### `Coupling4Param.tp`

This file contains information regarding the 4-monster synthesis recipes.

Each data block after the 4 bytes-long header is made of 10 bytes:
- 2 bytes for the monster species ID of the result
- 4\*2 bytes for each of the 4 monster species IDs of the components to synth together

IDs don't require any particular order.
 
## Changelog

Version 0
 - Made listed monsters available through generic synthesis, I don't know how the generic synthesis algorythm works, so expect ridiculous/expensive synthesis recipes to get some monsters.
 - Created somewhat basic documentation regarding the files that were modified.
Version 0.1
 - Monsters on the new list are now available through special synthesis, the corresponding 4-monster synthesis to obtain them is listed too.
   - These 4-monster recipes were made and reviewed with members of the community.
 - Updated documentation with new findings.
Version 0.2
  - Monsters that were previously listed here are now available through special synthesis only, the corresponding special synthesis to obtain them is listed too, in [SUMMARY.MD](./SUMMARY.MD).
   - These special recipes were made and reviewed with members of the community.
 - Updated documentation with new findings.
 
## Special thanks

- [**Lurpigi**](https://github.com/Lurpigi)

I started researching how it would be possible to add synthesis recipes after translating the technical documentation of your [randomizer](https://github.com/Lurpigi/DQMJ3P-Randomizer), which also helped me regarding what kind of data to look for.

- [**Anthcny**](https://github.com/Anthcny144)

You helped me search in the right direction when I was getting stuck when searching which files to edit to add synths.

- All the members of the community that helped me figure out the new synthesis recipes as well as sharing thoughts and critiques.

Immuno, Retho, RayGun! and Daddyvx from the [DQMJ3P English Discord server](https://discord.com/invite/W5yRJpDd5e).