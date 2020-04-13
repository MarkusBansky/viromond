cmake_minimum_required(VERSION 3.15)
project(viromod)

set(CMAKE_CXX_STANDARD 20)


find_package(glfw3 REQUIRED)
find_package(Corrade REQUIRED Main)
find_package(Magnum REQUIRED GL Shaders)
if(CORRADE_TARGET_APPLE)
    find_package(Magnum REQUIRED CglContext)
elseif(CORRADE_TARGET_UNIX)
    find_package(Magnum REQUIRED GlxContext)
elseif(CORRADE_TARGET_WINDOWS)
    find_package(Magnum REQUIRED WglContext)
else()
    message(FATAL_ERROR "No context handler available on this platform")
endif()

set_directory_properties(PROPERTIES CORRADE_USE_PEDANTIC_FLAGS ON)

# add executable file
add_executable(viromod src/main.cpp)

target_link_libraries(viromod PRIVATE
        glfw
        Corrade::Main
        Magnum::GL
        Magnum::GLContext
        Magnum::Magnum
        Magnum::Shaders)

# OpenGL
#find_package(OpenGL REQUIRED)
#target_link_libraries(viromod OpenGL::GL)
#
## GLFW
#target_link_libraries(viromod glfw)
#
## Magnum Project
#find_package(Magnum REQUIRED)
#target_link_libraries(viromod Magnum)
#
## SDL2 for Magnum
#find_package(SDL2 REQUIRED)
#include_directories(${SDL2_INCLUDE_DIRS})