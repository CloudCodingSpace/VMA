cmake_minimum_required(VERSION 3.30.0)
project(VMA)

file(GLOB_RECURSE SRCS CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp")
set(CMAKE_CXX_STANDARD 20)

find_package(Vulkan REQUIRED)

add_library(VMA ${SRCS})
target_compile_definitions(VMA PRIVATE
    $<$<CXX_COMPILER_ID:MSVC>:_CRT_SECURE_NO_WARNINGS>
)
target_compile_definitions(VMA PUBLIC
    VMA_STATIC_VULKAN_FUNCTIONS=1
    VMA_DYNAMIC_VULKAN_FUNCTIONS=0
)
target_include_directories(VMA PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")
target_link_libraries(VMA PUBLIC Vulkan::Vulkan)