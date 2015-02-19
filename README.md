# sdl2-mac-build

A simple Ruby based system to build SDL2 (and family) as dylibs for Mac OS X.

## Steps

    $ ./download
    $ ./build

## Details

The `download` script downloads the source packages for the libraries. This script sets up absolute paths to the files on the web so it's fragile and won't automatically get you the latest (if an update has come out since the script was updated). As such you can skip the script and download the `.tar.gz` source bundles manually from the project pages:

- [http://libsdl.org/download-2.0.php](http://libsdl.org/download-2.0.php).
- [https://www.libsdl.org/projects/SDL_image/](https://www.libsdl.org/projects/SDL_image/)
- [https://www.libsdl.org/projects/SDL_mixer/](https://www.libsdl.org/projects/SDL_mixer/)
- [https://www.libsdl.org/projects/SDL_net/](https://www.libsdl.org/projects/SDL_net/)
- [https://www.libsdl.org/projects/SDL_ttf/](https://www.libsdl.org/projects/SDL_ttf/)

While the download script will download all of these projects, only the main SDL2 project is required; each of the other libraries are optional and you can skip them if you have no use for them.

The `build` script then unzips the source archives to a temp directory before doing the builds. All dylibs are built as universal binaries for OS X 10.5 or higher (`-arch i386 -arch x86_64 -mmacosx-version-min=10.5`) and the script uses `install_name_tool` to fix up all paths so the dylibs are expected to be placed next to the executable in the app bundle.

## Caveat

While this has been working for me locally, admittedly I've yet to test these binaries on other machines or other versions of OS X. Make sure you do some testing of your application before distributing and don't blame me if this isn't perfect yet.
