cmake_minimum_required(VERSION 3.15)
set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_CXX_EXTENSIONS OFF)
if(UNIX)
    # Add file extension *.bin to all executables on Unix (Linux, OSX, BSD ...)
    set(CMAKE_EXECUTABLE_SUFFIX ".bin")
endif()

# set project and languages
project(viromod)
set(CMAKE_CXX_STANDARD 20)

# find open gl package
find_package(OpenGL REQUIRED)

# find glfw package
find_package(glfw3 REQUIRED)

# find glew package
find_package(GLEW REQUIRED)
if (GLEW_FOUND)
    include_directories(${GLEW_INCLUDE_DIRS})
    link_libraries(${GLEW_LIBRARIES})
endif()
set(GL_LIBRARY GL GLU X11)

add_definitions(
        -DTW_STATIC
        -DTW_NO_LIB_PRAGMA
        -DTW_NO_DIRECT3D
        -DGLEW_STATIC
        -D_CRT_SECURE_NO_WARNINGS
)

# add resources
file(DOWNLOAD "https://raw.githubusercontent.com/vector-of-bool/cmrc/master/CMakeRC.cmake"
        "${CMAKE_BINARY_DIR}/CMakeRC.cmake")
include("${CMAKE_BINARY_DIR}/CMakeRC.cmake")

cmrc_add_resource_library(
        viromod-resources

        ALIAS viromod::rc
        NAMESPACE viromod

        resources/simple_fragment_shader.fragmentshader
        resources/simple_vertex_shader.vertexshader
)

# add executable file
add_executable(viromod
        src/main.cpp
        src/common/shader.cpp
        src/common/shader.h)

# link libraries
target_link_libraries(viromod glfw GLEW::GLEW viromod::rc)