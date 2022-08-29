include(FetchContent)
FetchContent_Declare(
  GlewProxy
  URL https://github.com/nigels-com/glew/releases/download/glew-2.2.0/glew-2.2.0.tgz
  SOURCE_SUBDIR build/cmake
)
message(STATUS "Fetching GLEW ...")
FetchContent_MakeAvailable(GlewProxy)

add_library(glew_proxy INTERFACE)

if (${BUILD_SHARED_LIBS})
  message(STATUS "Using Shared GLEW")
  target_link_libraries(glew_proxy INTERFACE glew)
else()
  message(STATUS "Using Static GLEW")
  target_link_libraries(glew_proxy INTERFACE glew_s)
endif()

target_include_directories(glew_proxy INTERFACE "${PROJECT_BINARY_DIR}/_deps/glewproxy-src/include")
add_library(GLEW::GLEW ALIAS glew_proxy)

message(STATUS "Fetching GLEW ... done")