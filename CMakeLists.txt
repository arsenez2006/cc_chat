cmake_minimum_required(VERSION 3.18.0)
project(CyberCommunity_chat)

set(CMAKE_INSTALL_PREFIX ${CMAKE_CURRENT_SOURCE_DIR})
set(CMAKE_CXX_STANDARD 17)

if(NOT EXISTS "${CMAKE_BINARY_DIR}/conan.cmake")
    message(STATUS "Downloading conan.cmake...")
    file(DOWNLOAD "https://raw.githubusercontent.com/conan-io/cmake-conan/develop/conan.cmake" "${CMAKE_BINARY_DIR}/conan.cmake")
endif()
include(${CMAKE_BINARY_DIR}/conan.cmake)

conan_cmake_run(
    REQUIRES
        glfw/3.3.6
        imgui/1.87
    BUILD missing
    IMPORTS "./res/bindings, imgui_impl_opengl3* -> ${CMAKE_CURRENT_SOURCE_DIR}/client/imgui @ root_package=imgui"
    IMPORTS "./res/bindings, imgui_impl_glfw* -> ${CMAKE_CURRENT_SOURCE_DIR}/client/imgui @ root_package=imgui"
    BASIC_SETUP CMAKE_TARGETS
)

add_subdirectory(client)

install(TARGETS chat DESTINATION bin)