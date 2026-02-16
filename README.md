# Simgine

Simgine is a lightweight C++ simulation engine focused on deterministic 2D motion simulation and visualization.

The project is built using SDL2 for windowing and input handling, and OpenGL (core profile) for rendering. The engine is designed to keep simulation logic independent from rendering, allowing controlled experimentation with motion systems and time-stepped simulation models.

## Purpose

The primary goal of Simgine is to provide a minimal and deterministic environment for developing and testing 2D motion simulations. Rendering exists only as a visualization layer and must not influence simulation state.

The engine serves as a foundation for future systems such as collision detection, spatial partitioning, pathing, AI logic, and potentially a lightweight ECS architecture.

## Architecture Overview

The engine is structured around a fixed timestep simulation loop. Simulation runs at a constant update rate to ensure predictable and reproducible results. Rendering interpolates between simulation states where necessary.

A typical loop follows this model:

```cpp
while (running)
{
    accumulate_time();

    while (lag >= fixed_dt)
    {
        update_simulation(fixed_dt);
        lag -= fixed_dt;
    }
    render(interpolated_state);
}
```

## Simulation state and rendering state are explicitly separated.

The projected module layout is:

- Core  
- Simulation  
- Rendering  

Core handles application lifecycle, timing, and orchestration.  
Simulation manages world state, entities, and systems.  
Rendering handles visualization, shaders, camera logic, and debug drawing.

## Technology Stack

Language: C++20  
Windowing/Input: SDL2  
Rendering: OpenGL (Core Profile)  
Build System: CMake  
Platform: Linux (Artix / Arch)  

## Current Scope

The initial implementation focuses on establishing a clean foundation:

- Window and OpenGL context creation  
- Basic shader pipeline  
- 2D orthographic camera  
- Simple motion simulation using position and velocity  
- Debug visualization support  

## Build Instructions

Install dependencies on Artix / Arch:

```zsh
pacman -S sdl2 cmake clang mesa

# https://glad.dav1d.de/
# Language: C/C++
# Specification: OpenGL
# API: choose for example OpenGL 3.3
# Profile: Core
# Generate a loader: Yes
# Download zip
# unzip glad.zip
# move content to project

# Build the project:
mkdir build
cd build
cmake ..
cmake --build .

# Rebuild the project:
rm -rf build
mkdir build
cd build
cmake ..
cmake --build .

# Run the executable:
./simgine
```

## Development Direction

Simgine is currently in early development. Structure and APIs may change as the engine evolves.

Planned areas of exploration include deterministic replay, simple collision systems, spatial queries and modular system composition.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
