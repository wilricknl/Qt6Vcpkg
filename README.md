# Qt6 Vcpkg

A simple Qt6 Qt3D example using vcpkg and CMake.

### Vcpkg

I quite like to use vcpkg for package management, so this is a small experiment to get a Qt3D example up and running using vcpkg and CMake on Windows. First, install vcpkg as follows:

```shell
git clone https://github.com/microsoft/vcpkg.git
bootstrap-vcpkg.bat -disableMetrics
vcpkg integrate install
```

### Building

Simply open this project within Visual Studio 2022. It should automatically detect vcpkg and that this is a CMake project. The manifest file (`vcpkg.json`) will be used to download and install the required packages.

### CMake and Qt

In order to use Qt with CMake you need to define automoc for a specific target. This then will automatically apply the Qt magic to the source files. In this case I want to separate `scenemodifier.h` from the source code. Now automoc is not applied to this file, hence I still have to add `#include "moc_scenemodifier.cpp"` at the bottom of `scenemodifier.cpp`. This is not required if you put `scenemodifier.h` as a source file of the target.

Happy coding!
