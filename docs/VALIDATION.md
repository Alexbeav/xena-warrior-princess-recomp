# Xena: Warrior Princess validation receipt

## Scope

- Game: Xena: Warrior Princess, USA, `SLUS-00977`
- Version: `0.1.2`
- Catalog ID: `xena-warrior-princess-psx`
- Release repository: `Alexbeav/xena-warrior-princess-recomp`
- Publication state: public release `v0.1.2`

## Frozen inputs

- The source disc identity is in `catalog_identity.json`.
- The required BIOS is a legal SCPH-1001 dump. OpenBIOS is not supported.
- The complete owned CUE has one data track.
- Generated retail code, the game executable, the disc, and BIOS remain
  outside Git.

## Required release gates

The release candidate must pass generation, Release build, headless startup,
clean source package, payload, license, and clean-path checks. Alex must then
pass visible gameplay from the exact package.

## Local preparation evidence

- Studio audit: no required failure; two optional box-art warnings
- Code generation: 69 shards and 2,275 dispatch entries
- Full Release build: passed
- Hidden 25-second startup: frame and VBlank counts reached 2,977
- Fatal state: none
- Automatic or failed freeze dumps: none

The hidden test proves bounded startup progress. It does not prove full-game
correctness.

## RetComM package gate

RetComM `v0.6.33` installed the exact public Windows asset. Its SHA-256 is
`309479D31EED99A0146E9131F0C1A07328E356E48CA025A9DEE63E07053F035E`.
The package generated and built with an owned one-track USA disc and an owned
SCPH-1001 BIOS. Alex accepted gameplay from that installed package on
2026-09-04. A later RetComM launch skipped first-run setup, reached the game,
and closed through `sdl_window_close` at frame 1,700 with no fatal state.

The catalog manifest is `catalog/xena-warrior-princess-psx.json`. The hosted
form can misread the media-only `[netplay]` block as multiplayer support, so
leave the Netplay box clear.
