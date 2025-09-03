cmake_minimum_required(VERSION 3.10)
project(vulcan-voxel VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)

add_executable(vulcan-voxel main.cpp)

# Find Vulkan
find_package(Vulkan REQUIRED)
target_link_libraries(vulcan-voxel PRIVATE Vulkan::Vulkan)

# Find GLFW3 from Homebrew
find_package(glfw3 REQUIRED)
target_link_libraries(vulcan-voxel PRIVATE glfw)

# GLM via CPM (if you want system GLM, use find_package(glm REQUIRED) instead)
include(cmake/CPM.cmake)
CPMAddPackage("gh:g-truc/glm#1.0.1")
target_link_libraries(vulcan-voxel PRIVATE glm)