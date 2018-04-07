# ImguiDemoCLion

imgui + gl3w + SDL Hello World project in C++ (with CMake)

Compatible with CLion, Windows only for now

## Project structure

```bash
├───include
│       main.h
│
├───lib
│   ├───glew
│   │   ├───include
│   │   │   └───GL
│   │   │           *.h
│   │   │
│   │   └───src
│   │           *.c
│   │
│   ├───imgui
|   |       (imgui repository module)
│   │
│   ├───imgui_sdl
│   │       imgui_impl_sdl_gl3.cpp
│   │       imgui_impl_sdl_gl3.h
│   │
│   └───SDL2
│       ├───include
│       │   └───SDL2
│       │           *.h
│       └───lib
│               *.a
└───src
        main.cpp
```