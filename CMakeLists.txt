cmake_minimum_required(VERSION 3.1.3)

set(GLFW_SOURCE_DIR "external/glfw")
set(GLAD_SOURCE_DIR "external/glad")

# Building only the GLFW lib
set(BUILD_SHARED_LIBS OFF CACHE BOOL "")
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "")
set(GLFW_BUILD_TESTS OFF CACHE BOOL "")
set(GLFW_BUILD_DOCS OFF CACHE BOOL "")
set(GLFW_INSTALL OFF CACHE BOOL "")

add_subdirectory(${GLFW_SOURCE_DIR} ${GLAD_SOURCE_DIR})

include_directories(
        ${GLAD_SOURCE_DIR}/include
        ${GLFW_SOURCE_DIR}/include
        ${GLFW_SOURCE_DIR}/deps
)

add_library(glad STATIC
        ${GLAD_SOURCE_DIR}/src/glad.c
        ${GLAD_SOURCE_DIR}/include
        )

target_link_libraries(glad ${GLFW_LIBRARIES})

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)  # not necessary, but encouraged
set(APP_NAME "SceneManager")
add_executable(${APP_NAME} main.cpp)

target_link_libraries(${APP_NAME} glad glfw ${GLFW_LIBRARIES})