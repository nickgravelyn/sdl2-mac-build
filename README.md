# sdl2-mac-build

A simple Ruby based system to build SDL2 (and family) as dylibs for macOS.

## Steps

    $ ./download
    $ ./build

## Details

### Getting the source ready

The `download` script downloads the source packages for the libraries. This script sets up absolute paths to the files on the web so it's fragile and won't automatically get you the latest (if an update has come out since the script was updated). As such you can skip the script and download the `.tar.gz` source bundles manually from the project pages:

- [http://libsdl.org/download-2.0.php](http://libsdl.org/download-2.0.php)
- [https://www.libsdl.org/projects/SDL_image/](https://www.libsdl.org/projects/SDL_image/)
- [https://www.libsdl.org/projects/SDL_mixer/](https://www.libsdl.org/projects/SDL_mixer/)
- [https://www.libsdl.org/projects/SDL_net/](https://www.libsdl.org/projects/SDL_net/)
- [https://www.libsdl.org/projects/SDL_ttf/](https://www.libsdl.org/projects/SDL_ttf/)

While the download script will download all of these projects, only the main SDL2 project is required; each of the other libraries are optional and you can delete them if you have no use for them.

Alternatively you can create a `source` folder and clone each of the projects into there for building. Make sure the names match the canonical names (e.g. "SDL2", "SDL_image", etc). Then when you run the build you can pass `--from-source` to compile from source. This is handy in case there's a change that hasn't been released yet that you want.

### Building the source

The `build` script then unzips the source archives to a temp directory and produces universal builds supporting both `x86_64` and `arm64` architectures. The results are all placed into the `out` directory once the build is complete.

The dylibs are expected to be placed in the `Frameworks` directory of an app bundle per the [Anatomy of a macOS Application Bundle](https://developer.apple.com/library/archive/documentation/CoreFoundation/Conceptual/CFBundles/BundleTypes/BundleTypes.html#//apple_ref/doc/uid/10000123i-CH101-SW19) documentation and to align with the new code signing systems in macOS. If this is not how you plan to distribute the library, you'll probably want to use `install_name_tool` and change the `-id` of the libraries.

## Caveat

While this has been working for me locally, admittedly I've yet to test these binaries on other machines or other versions of macOS. Make sure you do some testing of your application before distributing and don't blame me if this isn't perfect yet.
