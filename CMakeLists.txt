cmake_minimum_required(VERSION 3.22)

project(
    "Opengltutorial1"
    VERSION 1.0.0
    LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake/)
set (VCPKG_DIR $ENV{VCPKG_ROOT})


message("CMAKE_MODULE_PATH = " ${CMAKE_MODULE_PATH})
message("VCPKG_DIR = " ${VCPKG_DIR})
message("PROJECT_NAME = " ${PROJECT_NAME})

include(${VCPKG_DIR}/scripts/buildsystems/vcpkg.cmake)

find_package(glfw3 CONFIG REQUIRED)
find_package(OpenGL REQUIRED)

add_executable(${PROJECT_NAME}
    src/main.cpp
    )

target_link_libraries(${PROJECT_NAME} PRIVATE glfw)
target_link_libraries(${PROJECT_NAME} PRIVATE OpenGL::GL)


message("PROJECT BIN DIR = "${PROJECT_BINARY_DIR})
message("PROJECT_NAME = " ${PROJECT_NAME})
message("CMAKE_COMMAND = " ${CMAKE_COMMAND})

add_custom_command(TARGET ${PROJECT_NAME}
  POST_BUILD
  COMMAND ${CMAKE_COMMAND} -E copy f:/devtools/opengl/opengl32.dll ${PROJECT_BINARY_DIR}/Debug
)