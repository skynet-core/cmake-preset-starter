cmake_minimum_required(VERSION 3.30)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
include(EnableCcache)

project(preset-template VERSION 1.0.0 LANGUAGES C CXX)

find_package(fmt CONFIG REQUIRED)

add_executable(app app/src/main.cpp)

target_link_libraries(app PRIVATE fmt::fmt-header-only)
