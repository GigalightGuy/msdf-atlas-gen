

file(GLOB_RECURSE MSDF_ATLAS_HEADERS RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "msdf-atlas-gen/*.h" "msdf-atlas-gen/*.hpp")
file(GLOB_RECURSE MSDF_ATLAS_SOURCES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "msdf-atlas-gen/*.cpp")

# msdf-atlas-gen library
add_library(msdf-atlas-gen ${MSDF_ATLAS_HEADERS} ${MSDF_ATLAS_SOURCES})
add_library(msdf-atlas-gen::msdf-atlas-gen ALIAS msdf-atlas-gen)
set_target_properties(msdf-atlas-gen PROPERTIES PUBLIC_HEADER "${MSDF_ATLAS_HEADERS}")
set_property(TARGET msdf-atlas-gen PROPERTY MSVC_RUNTIME_LIBRARY "${MSDF_ATLAS_MSVC_RUNTIME}")
target_compile_definitions(msdf-atlas-gen PUBLIC
    MSDF_ATLAS_VERSION=${MSDF_ATLAS_VERSION}
    MSDF_ATLAS_VERSION_MAJOR=${MSDF_ATLAS_VERSION_MAJOR}
    MSDF_ATLAS_VERSION_MINOR=${MSDF_ATLAS_VERSION_MINOR}
    MSDF_ATLAS_VERSION_REVISION=${MSDF_ATLAS_VERSION_REVISION}
    MSDF_ATLAS_COPYRIGHT_YEAR=${MSDF_ATLAS_COPYRIGHT_YEAR}
)
target_include_directories(msdf-atlas-gen INTERFACE
    $<INSTALL_INTERFACE:include>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
)
if(MSDF_ATLAS_NO_ARTERY_FONT)
    target_compile_definitions(msdf-atlas-gen PUBLIC MSDF_ATLAS_NO_ARTERY_FONT)
else()
    target_include_directories(msdf-atlas-gen PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/artery-font-format)
endif()
