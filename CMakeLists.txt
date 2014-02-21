project(gameclient.genplus)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(xbmc REQUIRED)

include(ExternalProject)

externalproject_add(genplus
                    GIT_REPOSITORY https://github.com/libretro/Genesis-Plus-GX
                    GIT_TAG d973d7d
                    PREFIX genplus
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND make -f Makefile.libretro
                    BUILD_IN_SOURCE 1)

set(GENPLUS_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/genplus/src/genplus/genesis_plus_gx_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                        genesis_plus_gx_libretro${CMAKE_SHARED_LIBRARY_SUFFIX} genplus)

build_addon(gameclient.genplus GENPLUS DEPLIBS)
add_dependencies(gameclient.genplus genplus)
