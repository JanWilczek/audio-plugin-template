cmake_minimum_required(VERSION 3.22)

project(WolfSoundAudioPluginTemplate)

set(CMAKE_CXX_STANDARD 23)

set(LIB_DIR ${CMAKE_CURRENT_SOURCE_DIR}/libs)
include(cmake/cpm.cmake)

# this commands downloads AND configures JUCE
CPMAddPackage(
    NAME JUCE
    GIT_TAG 7.0.5
    VERSION 7.0.5
    GITHUB_REPOSITORY juce-framework/JUCE
    SOURCE_DIR ${LIB_DIR}/juce
)

# Add googletest
CPMAddPackage(
    NAME GOOGLETEST
    GITHUB_REPOSITORY google/googletest
    GIT_TAG v1.13.0
    VERSION 1.13.0
    SOURCE_DIR ${LIB_DIR}/googletest
    OPTIONS
        "INSTALL_GTEST OFF"
        "gtest_force_shared_crt ON"
)

enable_testing()

if(MSVC)
    add_compile_options(/Wall /WX)
else()
    add_compile_options(-Wall -Wextra -Wpedantic)
endif()

add_subdirectory(plugin)
add_subdirectory(test)
