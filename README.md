# Wembley2D

**[Play it in your browser](https://jacksonlevine.github.io/wembley2d-web/)**

Wembley2D is a voxel sandbox game I wrote in C# with Unity in 2022. It was my first serious Unity project, and it is the project that eventually grew into [Distant Garden](https://store.steampowered.com/app/3114230), my C++ voxel game on Steam.

## The breakthrough

Before this project I assumed that splitting the world into chunks was an arbitrary design choice in voxel games. Building my own terrain taught me otherwise: chunking is what makes the whole thing fast enough to run.

Drawing every block as its own object falls over almost immediately. Grouping blocks into 16x16 columns and building one mesh per chunk means:

- the GPU draws a few hundred meshes instead of millions of cubes
- faces hidden between neighboring blocks are never generated
- breaking or placing a block only rebuilds the chunk it touches, plus its neighbors at the edges
- terrain can be generated and meshed a chunk at a time as the player moves, instead of all at once

Once that clicked, the rest of the game became possible. That same idea is the foundation of everything I have built in this space since.

## What is in it

- Procedural terrain built from Perlin noise, stored and meshed in chunks
- Runtime mesh generation with a queue that rebuilds chunks over several frames
- A day/night cycle with lighting and fog that change over time
- Custom shaders
- Breaking and placing blocks, an inventory and hotbar, and dropped items
- Mechanical parts: gears, levers, pipes, wells, and lanterns
- Trees, water, and randomly generated buildings

About 6,300 lines of C# across 27 scripts.

## Controls

| Input | Action |
|---|---|
| Click the game | Capture the mouse |
| Mouse | Look around |
| W A S D | Move |
| Space | Jump |
| Mouse buttons | Break and place blocks, use the selected item |
| Scroll wheel | Change hotbar slot |
| I | Open the inventory |
| Q | Drop the selected item |
| Esc | Release the mouse |

## From Wembley2D to Distant Garden

Wembley2D taught me how voxel worlds work. When I wanted more control over rendering, memory, and networking than Unity gave me, I moved to C++ and started again with those lessons in hand. The result is Distant Garden: a multiplayer 3D voxel game with a custom OpenGL renderer, released free on Steam in Early Access in August 2024.

- [Distant Garden on Steam](https://store.steampowered.com/app/3114230)
- [My GitHub profile](https://github.com/jacksonlevine)

## About this repository

This repository holds only the compiled WebGL build, served with GitHub Pages. The game was built with Unity 2021.3. For the browser version, the starting world is smaller than the desktop original so it fits in browser memory; more terrain generates as you explore.
