cmake_minimum_required(VERSION 3.20)
project(C++Engine CXX)

set(CMAKE_CXX_STANDARD 17)

# Vulkan SDK Pfad für macOS setzen
set(VULKAN_SDK "$ENV{HOME}/VulkanSDK/1.4.363.0/macOS")
set(ENV{Vulkan_ROOT} "${VULKAN_SDK}")

find_package(Vulkan REQUIRED)
find_package(glfw3 REQUIRED)

add_executable(C++Engine
    src/main.cpp
)

target_link_libraries(C++Engine PRIVATE Vulkan::Vulkan glfw)