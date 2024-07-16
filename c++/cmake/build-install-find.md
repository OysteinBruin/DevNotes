# Build, install and find a package with CMake

## Example 1 - Freetype library

https://download.savannah.gnu.org/releases/freetype/ freetype-2.13.2.tar.xz

unzip to folder, e.g. `C:/packages/freetype-2.13.2`

Generate build files with cmake:
open cmd in folder `C:/packages` and open Developeer Command Prompt for VS from dropdown menu

`cmake -S freetype-2.13.2 -B build-freetype-2.13.2`

Optional: Make cmake aware of dependencies: `cmake -S freetype-2.13.2 -B build-freetype-2.13.2 -DCMAKE_PREFIX_PATH=path/to/dependencies`

`cd build-freetype-2.13.2`

`cmake --build . --config Debug` (without using the VS build chain the build type can be specified with `-DCMAKE_BUILD_TYPE=Debug`)

Create cmake config file for find_package: `cmake --install . --config Debug --prefix C:\dev\_cpp-packages\freetype-2.13.2-msvc-debug`