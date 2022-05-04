cmake_minimum_required(VERSION 3.20)
project(Vulkan100K LANGUAGES CXX)

add_executable(Vulkan100K 
	"Source/main.cpp")
target_compile_features(Vulkan100K PRIVATE cxx_std_17)

file(RELATIVE_PATH RelEngineDir ${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})
target_compile_definitions(Vulkan100K PRIVATE ENGINE_DIR="${RelEngineDir}")

add_subdirectory(Vendor)
add_subdirectory(Shaders)
