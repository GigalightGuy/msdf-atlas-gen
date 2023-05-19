
add_subdirectory("msdfgen")

file(GLOB_RECURSE MSDF_ATLAS_HEADERS RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "msdf-atlas-gen/*.h" "msdf-atlas-gen/*.hpp")
file(GLOB_RECURSE MSDF_ATLAS_SOURCES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "msdf-atlas-gen/*.cpp")

# msdf-atlas-gen library
add_library(msdf-atlas-gen ${MSDF_ATLAS_HEADERS} ${MSDF_ATLAS_SOURCES})

target_include_directories(msdf-atlas-gen PRIVATE

    "msdf-atlas-gen"
	"msdfgen"
	"msdfgen/include"
)

target_link_libraries(msdf-atlas-gen PRIVATE 

	msdfgen 
)

target_compile_definitions(msdf-atlas-gen PRIVATE 

	_CRT_SECURE_NO_WARNINGS
)
