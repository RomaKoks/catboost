
# This file was gererated by the build system used internally in the Yandex monorepo.
# Only simple modifications are allowed (adding source-files to targets, adding simple properties
# like target_include_directories). These modifications will be ported to original
# ya.make files by maintainers. Any complex modifications which can't be ported back to the
# original buildsystem will not be accepted.



add_library(library-cpp-case_insensitive_string)
target_link_libraries(library-cpp-case_insensitive_string PUBLIC
  contrib-libs-cxxsupp
  yutil
  contrib-libs-libc_compat
  cpp-digest-murmur
)
target_sources(library-cpp-case_insensitive_string PRIVATE
  ${CMAKE_SOURCE_DIR}/library/cpp/case_insensitive_string/case_insensitive_char_traits.cpp
  ${CMAKE_SOURCE_DIR}/library/cpp/case_insensitive_string/case_insensitive_string.cpp
)
