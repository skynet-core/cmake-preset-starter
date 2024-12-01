cmake_minimum_required(VERSION 3.30)

if(NOT CMAKE_C_COMPILER_LAUNCHER OR NOT CMAKE_CXX_COMPILER_LAUNCHER)
    if(DEFINED ENV{ENABLE_CCACHE} OR DEFINED ENABLE_CCACHE)
        if(WIN32)
            find_program(CCACHE_EXECUTABLE "ccache.exe" CACHE PATH "ccache.exe path")
        else()
            find_program(CCACHE_EXECUTABLE ccache CACHE PATH "ccache path")
        endif()
        if(CCACHE_EXECUTABLE)
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
