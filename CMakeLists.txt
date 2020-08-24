# Minimum required CMake version and enforces that version policy settings,
# meaning CMake behaves like given version. First thing to put always!
cmake_minimum_required(VERSION 3.15)

# Project name.
project(cmake-examples)

add_subdirectory(loops)
add_subdirectory(variables)
