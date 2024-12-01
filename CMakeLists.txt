cmake_minimum_required(VERSION 3.30)

if("${CMAKE_C_COMPILER_LAUNCHER}" STREQUAL "" OR "${CMAKE_CXX_COMPILER_LAUNCHER}"
        STREQUAL "")
    if("$ENV{ENABLE_CCACHE}" STREQUAL "ON" OR "${ENABLE_CCACHE}" STREQUAL "ON")
        if(WIN32)
            find_program(CCACHE_EXECUTABLE "ccache.exe")
        else()
            find_program(CCACHE_EXECUTABLE ccache)
        endif()
        if(NOT "${CCACHE_EXECUTABLE}" STREQUAL "")
            set(CMAKE_C_COMPILER_LAUNCHER
                    ${CCACHE_EXECUTABLE}
                    CACHE PATH "Use ccache as C launcher")
            set(CMAKE_CXX_COMPILER_LAUNCHER
                    ${CCACHE_EXECUTABLE}
                    CACHE PATH "Use ccache as C++ launcher")
            message(STATUS "Found ccache ${CCACHE_EXECUTABLE}")
        else()
            message(WARNING "ccache not found")
        endif()
    endif()
endif()

project(preset-template VERSION 1.0.0 LANGUAGES C CXX)

find_package(fmt CONFIG REQUIRED)

add_executable(app app/src/main.cpp)

target_link_libraries(app PRIVATE fmt::fmt-header-only)
