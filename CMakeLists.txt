cmake_minimum_required(VERSION 3.16)
project(Simgine)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Find SDL2
find_package(SDL2 REQUIRED)

# Find OpenGL
find_package(OpenGL REQUIRED)

# Add include directories (GLAD and SDL2)
include_directories(
    include          # voor glad/glad.h
    ${SDL2_INCLUDE_DIRS}
)

# Add all source files
add_executable(app
    src/main.cpp
    src/glad.c
)

# Link libraries
target_link_libraries(app
    ${SDL2_LIBRARIES}
    ${OPENGL_gl_LIBRARY}
)
