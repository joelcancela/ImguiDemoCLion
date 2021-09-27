cmake_minimum_required(VERSION 3.10) # CMake minimum version
project(imguiExperiment) # Project name
set(CMAKE_CXX_STANDARD 11) # CPP version
set(APP_TARGET imguiExperiment) # Target Name
set(LIB_FOLDER ${CMAKE_CURRENT_SOURCE_DIR}/lib) # Lib folder
set(INCLUDE_FOLDER ${CMAKE_CURRENT_SOURCE_DIR}/include) # Include folder

# Libs
## Imgui lib
set(imgui_Includes "${LIB_FOLDER}/imgui/")
add_library(imgui STATIC
        ${LIB_FOLDER}/imgui/imgui.cpp
        ${LIB_FOLDER}/imgui/imgui_draw.cpp
        ${LIB_FOLDER}/imgui/imgui_demo.cpp
        ${LIB_FOLDER}/imgui/imgui_tables.cpp
        ${LIB_FOLDER}/imgui/imgui_widgets.cpp)

## SDL2
set(SDL2_Flags "-mwindows -Wl,--no-undefined -static-libgcc")
set(SDL2_ROOT "${LIB_FOLDER}/SDL2/i686-w64-mingw32")
set(SDL2_Includes "${SDL2_ROOT}/include/SDL2")
set(SDL2_LibDir "${SDL2_ROOT}/lib")
add_library(SDL2 STATIC IMPORTED)
add_library(SDL2main STATIC IMPORTED)
set_property(TARGET SDL2 PROPERTY IMPORTED_LOCATION "${SDL2_LibDir}/libSDL2.a")
set_property(TARGET SDL2main PROPERTY IMPORTED_LOCATION "${SDL2_LibDir}/libSDL2main.a")

## Glew
set(glew_Includes "${LIB_FOLDER}/glew/include")
add_library(glew STATIC
        ${LIB_FOLDER}/glew/src/gl3w.c)

## Imgui SDL lib
set(imgui-sdl_Includes "${LIB_FOLDER}/imgui_sdl/")
add_library(imgui-sdl STATIC
        ${LIB_FOLDER}/imgui_sdl/imgui_impl_sdl_gl3.cpp)


# Compilation
set(SDL2_Libs mingw32 SDL2 SDL2main m dinput8 dxguid dxerr8 hid setupapi user32 gdi32 winmm imm32 ole32 oleaut32 shell32 version uuid) # Libs for windows only
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 ${SDL2_Flags}") # Compiler flags
include_directories(${INCLUDE_FOLDER} ${SDL2_Includes} ${glew_Includes} ${imgui-sdl_Includes} ${imgui_Includes}) # Include folders
set(SOURCE_FILES src/main.cpp) # Source files
add_executable(${APP_TARGET} ${SOURCE_FILES}) # Executable
target_include_directories(${APP_TARGET} SYSTEM PRIVATE ${SDL2_Includes}) # Include SDL headers
target_link_libraries(${APP_TARGET} ${SDL2_LIBRARY} ${SDL2_Libs} imgui glew imgui-sdl) # Linker folders