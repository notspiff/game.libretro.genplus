project(game.libretro.genplus)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(Kodi REQUIRED)
find_package(libretro-genplus REQUIRED)

set(DEPLIBS genplus)
set(GENPLUS_CUSTOM_BINARY ${GENPLUS_LIB}
                          game.libretro.genplus${CMAKE_SHARED_LIBRARY_SUFFIX} genplus)

build_addon(game.libretro.genplus GENPLUS DEPLIBS)

