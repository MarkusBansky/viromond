cmake_minimum_required(VERSION 3.15)

# set project and languages
project(viromod)
set(CMAKE_CXX_STANDARD 20)

# find packages
# find open gl package
find_package(OpenGL REQUIRED)

if(NOT OPENGL_FOUND)
    message("ERROR: OpenGL not found")
endif(NOT OPENGL_FOUND)

# find glfw package
find_package(glfw3 REQUIRED)

# find glew package
find_package(GLEW REQUIRED)
if (GLEW_FOUND)
    include_directories(${GLEW_INCLUDE_DIRS})
    link_libraries(${GLEW_LIBRARIES})
else()
    message("ERROR: GLEW not found")
endif()
set(GL_LIBRARY GL GLU X11)

# add executable file
add_executable(viromod src/main.cpp src/common/shader.cpp src/common/shader.h)

# link libraries
target_link_libraries(viromod glfw GLEW)