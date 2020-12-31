cmake_minimum_required(VERSION 3.12 FATAL_ERROR)

# Set project name and version
project(Pong VERSION 1.0)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)

# Enable debug symbols by default
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug 
    CACHE STRING 
      "Choose the type of build (Debug or Release)" FORCE)
endif()

# Export compile commands for completion engines (optional)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Path to load resources from
set(RESOURCE_PATH "${PROJECT_SOURCE_DIR}/content/")

# Generate config.h
configure_file(include/config.h.in config.h)

# Find SFML shared libraries
add_subdirectory(external/SFML-2.5.1)

# Find Box2D shared libraries
add_subdirectory(external/box2d-2.4.1)

# Compile executable
add_executable(Pong
        src/main.cpp
        src/Ball.cpp
        src/Bat.cpp)

# Set include directory search paths
target_include_directories(Pong 
  PRIVATE
    "${PROJECT_BINARY_DIR}"
    "${CMAKE_CURRENT_SOURCE_DIR}/include"
  )

# Link executable to required SFML modules
target_link_libraries(Pong sfml-graphics sfml-audio box2d)
