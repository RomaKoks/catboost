
# This file was gererated by the build system used internally in the Yandex monorepo.
# Only simple modifications are allowed (adding source-files to targets, adding simple properties
# like target_include_directories). These modifications will be ported to original
# ya.make files by maintainers. Any complex modifications which can't be ported back to the
# original buildsystem will not be accepted.


cmake_minimum_required(VERSION 3.15)
project(CATBOOST LANGUAGES ASM C CXX)

set(BUILD_SHARED_LIBS Off)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_EXTENSIONS Off)
set(CATBOOST_MAX_LINK_JOBS 5 CACHE STRING "Maximum parallel link jobs for Ninja generator")
set_property(GLOBAL PROPERTY JOB_POOLS link_jobs=${CATBOOST_MAX_LINK_JOBS})
set(CMAKE_JOB_POOL_LINK link_jobs)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_BINARY_DIR} ${CMAKE_SOURCE_DIR}/cmake)
include_directories(${CMAKE_SOURCE_DIR} ${CMAKE_BINARY_DIR})
list(APPEND CMAKE_CTEST_ARGUMENTS "--output-on-failure")
enable_testing()
include(cmake/archive.cmake)
include(cmake/conan.cmake)
include(cmake/cython.cmake)
include(cmake/fat_object.cmake)
include(cmake/fbs.cmake)
include(cmake/global_flags.cmake)
include(cmake/protobuf.cmake)
include(cmake/swig.cmake)
include(cmake/yandex_common.cmake)
include(cmake/global_vars.cmake)

conan_cmake_configure(
  GENERATORS cmake_find_package
  REQUIRES
    openssl/1.1.1l
    ragel/6.10
    swig/4.0.2
    yasm/1.3.0
    zlib/1.2.12
  IMPORTS
    "bin, *swig* -> ./bin"
    "bin, *yasm* -> ./bin"
    "bin, ragel* -> ./bin"
    "bin, ytasm* -> ./bin"
)
conan_cmake_autodetect(settings)
conan_cmake_install(
  PATH_OR_REFERENCE .
  BUILD missing
  REMOTE conancenter
  SETTINGS ${settings}
)

if (UNIX AND NOT APPLE)
  include(CMakeLists.linux.txt)
elseif (APPLE)
  include(CMakeLists.darwin.txt)
endif()
