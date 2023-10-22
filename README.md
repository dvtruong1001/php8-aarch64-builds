# THIS REPO RELEASED PM5 FOR ARM64 - WARNING. PM4 is deprecated. So new releases are getting only PM5
### last release / new release https://github.com/TukangM/php8-aarch64-builds/releases/latest
### last support pm4 at this release https://github.com/TukangM/php8-aarch64-builds/releases/tag/php8.1.23

## compile.sh

Bash script used to compile PHP on MacOS and Linux platforms. Make sure you have ``make autoconf automake libtool m4 wget getconf gzip bzip2 bison g++ git cmake pkg-config re2c``.

### Additional notes
#### Mac OSX (native compile)
- Most dependencies can be installed using Homebrew
- You will additionally need `glibtool` (GNU libtool, xcode libtool won't work)
- You also MUST specify target as `mac` or `mac64` if building for Mac, on Mac.

#### Android 64-bit (cross-compile)
- Only aarch64 targets are supported for Android cross-compile.
- The `aarch64-linux-musl` toolchain is required. You can compile and install it using https://github.com/pmmp/musl-cross-make (PMMP fork includes musl-libc patches for DNS resolver config path and increasing stack size limit for LevelDB)

| Script flags | Description                                                                                                 |
|--------------|-------------------------------------------------------------------------------------------------------------|
| -c           | Uses the folder specified for caching downloaded tarballs, zipballs etc.                                    |
| -d           | Compiles with debugging symbols and disables optimizations (slow, but useful for debugging segfaults)       |
| -D           | Compiles with separated debugging symbols, but leaves optimizations enabled (used for distributed binaries) |
| -g           | Will compile GD2                                                                                            |
| -j           | Set make threads to #                                                                                       |
| -l           | Uses the folder specified for caching compilation artifacts (useful for rapid rebuild and testing)          |
| -n           | Don't remove sources after completing compilation                                                           |
| -s           | Will compile everything statically                                                                          |
| -t           | Set target                                                                                                  |
| -v           | Enable Valgrind support in PHP                                                                              |
| -x           | Specifies we are doing cross-compile                                                                        |
| -P           | Compiles extensions for the major PocketMine-MP version specified (can be `4` or `5`)                       |

### Example:

| Target          | Arguments                         |
|-----------------|-----------------------------------|
| linux64         | ``-t linux64 -j4 -P5``            |
| linux64, PM4    | ``-t linux64 -j4 -P4``            |
| mac64           | ``-t mac-x86-64 -j4 -P5``         |
| android-aarch64 | ``-t android-aarch64 -x -j4 -P5`` |

## windows-compile-vs.bat

Batch script utilizing Visual Studio on Windows to compile PHP binaries from sources.
Ensure you have Visual Studio 2019, `git`, `7z` and `wget` installed in your PATH.

This script doesn't accept parameters, but the following environment variables are influential:

| Variable | Description                                                                                                        |
| -------- |--------------------------------------------------------------------------------------------------------------------|
| `PHP_DEBUG_BUILD` | Disables optimisations and builds PHP with detailed debugging information (useful for debugging segfaults)|
| `SOURCES_PATH` | Where to put the downloaded sources for compilation                                                          |
| `VS_EDITION` | Edition of Visual Studio installed, set to `Community` by default                                              |
| `PM_VERSION_MAJOR` | Major version of PocketMine-MP to build extensions for (defaults to 4, can be `4` or `5`)                |
