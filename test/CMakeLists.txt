cmake_minimum_required(VERSION 3.22)

project(AudioPluginTest)

# Signals to CMake that we want to run tests from this directory.
enable_testing()

# Creates the test console application.
add_executable(${PROJECT_NAME}
    source/AudioProcessorTest.cpp)

# Sets the necessary include directories: ours, JUCE's, and googletest's.
target_include_directories(${PROJECT_NAME}
    PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/../plugin/include
        ${JUCE_SOURCE_DIR}/modules
        ${GOOGLETEST_SOURCE_DIR}/googletest/include)

# Thanks to the fact that we link against the gtest_main library, we don't have to write the main function ourselves.
target_link_libraries(${PROJECT_NAME}
    PRIVATE
        AudioPlugin
        GTest::gtest_main)

# Adds googletest-specific CMake commands at our disposal.
include(GoogleTest)
# Add all tests defined with googletest to the CMake metadata so that these tests are run upon a call to ctest in the test projects' binary directory.
gtest_discover_tests(${PROJECT_NAME})
