file(GLOB_RECURSE GLSL_SOURCE_FILES
	"${PROJECT_SOURCE_DIR}/Shaders/*.frag"
	"${PROJECT_SOURCE_DIR}/Shaders/*.vert"
	"${PROJECT_SOURCE_DIR}/Shaders/*.comp")

foreach(GLSL ${GLSL_SOURCE_FILES})
	get_filename_component(FILE_NAME ${GLSL} NAME)
	set(SPIRV "${PROJECT_SOURCE_DIR}/Shaders/${FILE_NAME}.spv")
	add_custom_command(OUTPUT ${SPIRV}
		COMMAND ${Vulkan_GLSLANG_VALIDATOR_EXECUTABLE} -V ${GLSL} -o ${SPIRV}
		DEPENDS ${GLSL}
		VERBATIM)
	set_source_files_properties(${SPIRV} PROPERTIES GENERATED TRUE)
	list(APPEND SPIRV_BINARY_FILES ${SPIRV})
endforeach()

source_group(GLSL FILES ${GLSL_SOURCE_FILES})
add_custom_target(Shaders 
	SOURCES ${GLSL_SOURCE_FILES} 
	DEPENDS ${SPIRV_BINARY_FILES})
add_dependencies(Vulkan100K Shaders)
