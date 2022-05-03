cmake_minimum_required(VERSION 3.20)
project(Vulkan100K LANGUAGES CXX)

add_executable(Vulkan100K 
	"Source/main.cpp")

add_subdirectory(Vendor)
add_subdirectory(Shaders)
