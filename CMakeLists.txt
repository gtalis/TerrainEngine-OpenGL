cmake_minimum_required(VERSION 2.6)

project(TerrainEngine-OpenGL
	DESCRIPTION "An OpenGL 4 and C++ program which renders a procedural scene. "
	HOMEPAGE_URL "https://github.com/fede-vaccaro/TerrainEngine-OpenGL")
	
file(GLOB sources
	Compile/*.cpp
	Compile/*.c
	Engine/*.cpp
	DrawableObjects/*.cpp
	imgui/*.cpp
	Main.cpp
)
list(REMOVE_ITEM sources "${CMAKE_SOURCE_DIR}/Engine/shaderUtils.cpp")

# External dependencies
find_package(PkgConfig REQUIRED)
# OpenGL
find_package(OpenGL REQUIRED)
# glfw
pkg_check_modules(GLFW glfw3 REQUIRED)

include_directories(
	${CMAKE_CURRENT_SOURCE_DIR}/Include
	${CMAKE_CURRENT_SOURCE_DIR}/imgui
	${GLFW_INCLUDE_DIRS}
	${OPENGL_INCLUDE_DIRS}
)

add_executable (TerrainEngine ${sources})
target_link_libraries(TerrainEngine ${GLFW_LIBRARIES} ${OPENGL_LIBRARY} ${CMAKE_DL_LIBS})
