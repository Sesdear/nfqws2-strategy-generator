cmake_minimum_required(VERSION 3.16)
project(nfqws2-strategy-gen LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_BUILD_TYPE Release)

add_executable(nfqws2-strategy-gen
    src/main.cpp
    src/generator.cpp
)

target_include_directories(nfqws2-strategy-gen PRIVATE src)

target_compile_options(nfqws2-strategy-gen PRIVATE
    -O3 -fno-exceptions -fno-rtti)

target_link_options(nfqws2-strategy-gen PRIVATE
    -static-libgcc -static-libstdc++)
