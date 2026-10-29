cmake_minimum_required(VERSION 3.20)
project(C++Engine CXX)

set(CMAKE_CXX_STANDARD 17)

# Vulkan SDK Pfad für macOS setzen
set(VULKAN_SDK "$ENV{HOME}/VulkanSDK/1.4.363.0/macOS")
set(ENV{Vulkan_ROOT} "${VULKAN_SDK}")

find_package(Vulkan REQUIRED)
find_package(glfw3 REQUIRED)

# --- Shader Automatisierung ---
set(SHADER_DIR "${CMAKE_CURRENT_SOURCE_DIR}/shaders") # Passe den Pfad an falls nötig
set(VERT_SRC "${SHADER_DIR}/shader.vert")
set(FRAG_SRC "${SHADER_DIR}/shader.frag")
set(VERT_SPV "${CMAKE_CURRENT_BINARY_DIR}/vert.spv")
set(FRAG_SPV "${CMAKE_CURRENT_BINARY_DIR}/frag.spv")

# glslc Pfad aus dem Vulkan SDK ableiten
set(GLSLC "${VULKAN_SDK}/bin/glslc")

# Custom Commands, die glslc nur ausführen, wenn sich die Shader geändert haben
add_custom_command(
    OUTPUT ${VERT_SPV}
    DEPENDS ${VERT_SRC}
    COMMAND ${GLSLC} ${VERT_SRC} -o ${VERT_SPV}
    COMMENT "Kompiliere Vertex-Shader..."
)

add_custom_command(
    OUTPUT ${FRAG_SPV}
    DEPENDS ${FRAG_SRC}
    COMMAND ${GLSLC} ${FRAG_SRC} -o ${FRAG_SPV}
    COMMENT "Kompiliere Fragment-Shader..."
)

# Ein eigenes Target für die Shader, damit CMake sie baut
add_custom_target(CompileShaders DEPENDS ${VERT_SPV} ${FRAG_SPV})
# -----------------------------

add_executable(C++Engine
    src/main.cpp
)

# Sorge dafür, dass die Shader kompiliert werden, BEVOR die Executable gebaut wird
add_dependencies(C++Engine CompileShaders)

target_link_libraries(C++Engine PRIVATE Vulkan::Vulkan glfw)