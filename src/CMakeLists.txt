# The Flutter tooling requires that developers have CMake 3.10 or later
# installed. You should not increase this version, as doing so will cause
# the plugin to fail to compile for some customers of the plugin.
cmake_minimum_required(VERSION 3.10)

project(demo_library_library VERSION 0.0.1 LANGUAGES C)

add_library(demo_library SHARED
  "demo_library.c"
)

set_target_properties(demo_library PROPERTIES
  PUBLIC_HEADER demo_library.h
  OUTPUT_NAME "demo_library"
)

target_compile_definitions(demo_library PUBLIC DART_SHARED_LIB)

if (ANDROID)
  # Support Android 15 16k page size
  target_link_options(demo_library PRIVATE "-Wl,-z,max-page-size=16384")
endif()
