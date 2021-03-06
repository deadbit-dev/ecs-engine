cmake_minimum_required(VERSION 3.10)
project(ecs-engine VERSION 0.0.2)

# =============================================================================
# Variables
# =============================================================================
set(DIR_THIRDPARTY ${CMAKE_CURRENT_SOURCE_DIR}/3rdparty)
set(DIR_EXPORT ${CMAKE_CURRENT_SOURCE_DIR}/build/${CMAKE_BUILD_TYPE})
set(DIR_ENGINE_API ${CMAKE_CURRENT_SOURCE_DIR}/include)

if (WIN32)
	set(ENGINE_PLATFORM windows)
	set(ENGINE_ABI x64)
endif()

if(APPLE)
	set(ENGINE_PLATFORM macos)
	set(ENGINE_ABI x64)
endif()

if(UNIX AND NOT APPLE)
	set(ENGINE_PLATFORM linux)
	set(ENGINE_ABI x64)
endif()

# =============================================================================
# General compile flags
# =============================================================================
if (WIN32)
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /std:c++17 /Zc:__cplusplus")
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /D_SILENCE_CXX17_ITERATOR_BASE_CLASS_DEPRECATION_WARNING")
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /D_CRT_SECURE_NO_WARNINGS")
else()
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -fstrict-aliasing -Wno-unknown-pragmas -Wno-unused-function")
endif()

# =============================================================================
# General includes
# =============================================================================
include_directories("3rdparty/")
include_directories("3rdparty/entt/single_include")
include_directories("3rdparty/glfw/include")
include_directories("3rdparty/volk")
include_directories("3rdparty/vulkan")

# =============================================================================
# General libraries
# =============================================================================
link_directories("3rdparty/glfw/lib")

# =============================================================================
# Sub-projects
# =============================================================================
add_subdirectory(source/core)
add_subdirectory(source/glfw_window)
add_subdirectory(source/vk_render)
add_subdirectory(source/app)