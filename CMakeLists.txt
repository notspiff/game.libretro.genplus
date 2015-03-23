project(game.libretro.genplus)

cmake_minimum_required(VERSION 2.6)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(kodi REQUIRED)

if(CMAKE_BUILD_TYPE MATCHES Debug)
  set(LIBRETRO_DEBUG DEBUG=1)
endif()

if("${CORE_SYSTEM_NAME}" STREQUAL "windows")
  set(BUILD_COMMAND mingw32-make -f Makefile.libretro platform=win ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "linux")
  set(BUILD_COMMAND make -f Makefile.libretro ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "darwin")
  set(BUILD_COMMAND make -f Makefile.libretro platform=osx ${LIBRETRO_DEBUG})
elseif("${CORE_SYSTEM_NAME}" STREQUAL "ios")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "android")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "rbpi")
  # TODO
elseif("${CORE_SYSTEM_NAME}" STREQUAL "freebsd")
# TODO
endif()

include(ExternalProject)
externalproject_add(genplus
                    GIT_REPOSITORY https://github.com/libretro/Genesis-Plus-GX
                    GIT_TAG d973d7d
                    PREFIX genplus
                    CONFIGURE_COMMAND ""
                    INSTALL_COMMAND ""
                    BUILD_COMMAND ${BUILD_COMMAND}
                    BUILD_IN_SOURCE 1)

set(GENPLUS_CUSTOM_BINARY ${PROJECT_BINARY_DIR}/genplus/src/genplus/genesis_plus_gx_libretro${CMAKE_SHARED_LIBRARY_SUFFIX}
                          game.libretro.genplus${CMAKE_SHARED_LIBRARY_SUFFIX} genplus)

build_addon(game.libretro.genplus GENPLUS DEPLIBS)
add_dependencies(game.libretro.genplus genplus)

include(CPack)
