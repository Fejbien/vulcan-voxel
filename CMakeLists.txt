cmake_minimum_required(VERSION 3.10)
project(vulcan-voxel VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)

add_executable(vulcan-voxel main.cpp)

# Find Vulkan
find_package(Vulkan REQUIRED)
target_link_libraries(vulcan-voxel PRIVATE Vulkan::Vulkan)

# Find GLFW3 from Homebrew
find_package(glfw3 REQUIRED)
# Use the modern imported target "glfw::glfw" if available, otherwise fallback to glfw
if(TARGET glfw::glfw)
	target_link_libraries(vulcan-voxel PRIVATE glfw::glfw)
elseif(TARGET glfw)
	target_link_libraries(vulcan-voxel PRIVATE glfw)
else()
	message(FATAL_ERROR "GLFW target not found. Please check your glfw3 installation.")
endif()

# GLM via CPM
include(cmake/CPM.cmake)
CPMAddPackage("gh:g-truc/glm#1.0.1")
target_link_libraries(vulcan-voxel PRIVATE glm)