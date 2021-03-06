# CMakeLists files in this project can
# refer to the root source directory of the project as ${HELLO_SOURCE_DIR} and
# to the root binary directory of the project as ${HELLO_BINARY_DIR}.
cmake_minimum_required (VERSION 3.1)

# Enable ExternalProject CMake module
include(ExternalProject)

# Set default ExternalProject root directory
set_directory_properties(PROPERTIES EP_PREFIX ${CMAKE_BINARY_DIR}/target)

project (binding)

add_library (binding SHARED src/binding.cc)
target_include_directories (${PROJECT_NAME} PUBLIC ${CMAKE_SOURCE_DIR}/src/napi_sys)
target_compile_options(binding PUBLIC -std=c++11 )

if (UNIX)
target_link_libraries(${PROJECT_NAME}
  debug "${CMAKE_SOURCE_DIR}/target/debug/libssb_legacy_msg_js.a"
  optimized "${CMAKE_SOURCE_DIR}/target/release/libssb_legacy_msg_js.a"
)
endif (UNIX)

if (WIN32)
target_link_libraries(${PROJECT_NAME}
  debug "${CMAKE_SOURCE_DIR}/target/debug/ssb_legacy_msg_js.lib"
  optimized "${CMAKE_SOURCE_DIR}/target/release/ssb_legacy_msg_js.lib"
)
endif (WIN32)
