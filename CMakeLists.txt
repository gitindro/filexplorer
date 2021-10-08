cmake_minimum_required(VERSION 3.12)

project(xplorer)

include(CMakeCommon/CommonMacros.txt)

set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "")
set(GLFW_BUILD_TESTS OFF CACHE BOOL "")
set(GLFW_BUILD_DOCS OFF CACHE BOOL "")
set(GLFW_INSTALL OFF CACHE BOOL "")

if(WIN32)
	add_definitions(-D_CRT_SECURE_NO_WARNINGS)
endif()

#include_directories(deps/src/vulkan/include)
add_subdirectory(deps/src/glfw)


set(GLAD_SOURCES deps/glad/src/gl.c dependencies/glad/src/vulkan.c)
if(WIN32)
	set(GLAD_SOURCES ${GLAD_SOURCES} dependencies/glad/src/wgl.c)
endif()
add_library(glad ${GLAD_SOURCES})

include_directories(deps/src/glfw/include)
include_directories(deps/glad/include)
#include_directories(deps/src/glm)


set_property(TARGET glfw            PROPERTY FOLDER "ThirdPartyLibraries")
set_property(TARGET glad            PROPERTY FOLDER "ThirdPartyLibraries")


SETUP_APP(xplorer_cmake "xplorer")


target_link_libraries(xplorer_cmake glad glfw)