# Bloody Roar PSXRecomp

This is an unofficial Bloody Roar PSX recompilation project for the USA
release (serial `SCUS-94199`). It is a source/setup-host repository only.

No game files, ROMs, disc images, BIOS files, copyrighted game assets, or
generated game code are included. Generated recompilation code remains local
in the ignored `generated/` directory. The repository uses mstan's
[PSXRecomp](https://github.com/mstan/psxrecomp) framework and the
[recomp-ui](https://github.com/mstan/recomp-ui) launcher as Git submodules.

The project is not claimed to be complete or playable. Runtime behavior must
be verified locally after generating code from a legally obtained disc.

## Clone

```bash
git clone --recurse-submodules https://github.com/omegakatana92/Bloody-Roar.git
cd Bloody-Roar
```

## Legal input

Users must supply their own legally obtained USA Bloody Roar disc dump. Keep
the cue/bin files and any retail BIOS outside Git; the paths in `game.toml`
describe local inputs only. Do not upload disc data, BIOS dumps, extracted game
files, generated C, or promotional artwork.

## Generate and build

The documented PSXRecomp setup-host workflow is:

1. Build the recompiler emitters once, or after framework changes:

	```bash
	./psxrecomp/tools/ci/build_emitters.sh
	```

2. Generate game and OpenBIOS C locally from your own disc:

	```bash
	python3 psxrecomp/psxrecomp_cli.py generate \
		 --config game.toml --project-root . --disc "disc/Bloody Roar (USA).cue"
	```

3. Configure and build the local runtime:

	```bash
	cmake -S . -B build-release -G Ninja -DCMAKE_BUILD_TYPE=Release
	cmake --build build-release --target psx-runtime
	```

The setup wizard provided by recomp-ui can also run Generate and rebuild when
the runtime is configured with `PSX_SETUP_WIZARD=ON`. Build directories,
generated C, saves, logs, and all disc/BIOS material are intentionally ignored.

## Project metadata

`game.toml` contains configuration and verification hashes only. The seed file
contains address lists only. These files do not embed game data.