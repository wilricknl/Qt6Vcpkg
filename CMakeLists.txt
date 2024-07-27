cmake_minimum_required(VERSION 3.20)

set(Qt6Vcpkg_VERSION 1.0.0)

project(Qt6Vcpkg
        VERSION ${Qt6Vcpkg_VERSION}
        DESCRIPTION "Qt6 Vcpkg Example"
        HOMEPAGE_URL "https://github.com/wilricknl/Qt6Vcpkg"
        LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)

include(CMakePackageConfigHelpers)
include(GNUInstallDirs)

## Interpret source as utf-8 on Windows to ensure
## non-ascii characters are read properly.
add_compile_options("$<$<C_COMPILER_ID:MSVC>:/utf-8>")
add_compile_options("$<$<CXX_COMPILER_ID:MSVC>:/utf-8>")

## Static builds on Windows
if (MSVC)
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
endif()

# -----------------------------------------------------------------------------
# DEPENDENCIES
# -----------------------------------------------------------------------------

find_package(Qt6Core CONFIG REQUIRED)
find_package(Qt6Widgets CONFIG REQUIRED)
find_package(Qt63DAnimation CONFIG REQUIRED)
find_package(Qt63DCore CONFIG REQUIRED)
find_package(Qt63DExtras CONFIG REQUIRED)
find_package(Qt63DInput CONFIG REQUIRED)
find_package(Qt63DLogic CONFIG REQUIRED)
find_package(Qt63DRender CONFIG REQUIRED)

# -----------------------------------------------------------------------------
# Includes
# -----------------------------------------------------------------------------

include_directories(include)

# -----------------------------------------------------------------------------
# Executable
# -----------------------------------------------------------------------------

add_executable(qt6vcpkg src/main.cpp src/scenemodifier.cpp)
target_link_libraries(qt6vcpkg PRIVATE Qt6::Core Qt6::Widgets Qt::3DAnimation Qt::3DCore Qt::3DExtras Qt::3DInput Qt::3DLogic Qt::3DRender)
set_property(TARGET qt6vcpkg PROPERTY AUTOMOC ON)

# -----------------------------------------------------------------------------
# INSTALLATION
# -----------------------------------------------------------------------------

install(TARGETS qt6vcpkg)
