cmake_minimum_required(VERSION 3.18.X)
project(GLFWtriangle-vulkan_Project LANGUAGES C)
add_executable(GLFWtriangle-vulkan triangle-vulkan.c)
target_compile_features(GLFWtriangle-vulkan PRIVATE c_std_11)

set(CMAKE_BUILD_TYPE debug)

# -----------------------------------------------------
# (*) brew install glfw3 --HEAD
# (*) LunarG SDK Vulkan

#Finding and linking GLFW3 (windowing, context & input)
find_package(GLFW3 3.3 REQUIRED)
if (GLFW3_FOUND)
    message("GLFW3 FOUND")
    target_link_libraries(GLFWtriangle-vulkan glfw)
endif (GLFW3_FOUND)

#Linker need GLAD library
# https://gen.glad.sh generate vulkan.h 
# No need to try https://glad.dav1d.de, it does not have vulkan.
# Remember Do not tick header only, the linker needs the C file
add_library(GLAD "libs/GLAD/vulkan.c")
target_link_libraries(GLFWtriangle-vulkan GLAD)

#For include <glad/vulkan.h> in triangle-vulkan.c
target_include_directories(GLFWtriangle-vulkan
   PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/libs"
   )

