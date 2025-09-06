cmake_minimum_required(VERSION 3.10)
project(LlamaSimpleProject CXX CUDA)

set(TARGET llama-simple)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(CUDA REQUIRED COMPONENTS cublas)
find_package(OpenMP REQUIRED)
find_package(Threads REQUIRED)

add_executable(${TARGET} simple.cpp)

target_include_directories(${TARGET} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/include
)

target_link_directories(${TARGET} PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/lib
)

target_link_libraries(${TARGET} PRIVATE
    llama
    ggml
    ggml-base
    ggml-cpu
    ggml-cuda

    OpenMP::OpenMP_CXX

    ${CUDA_LIBRARIES}        # Links to cudart
    ${CUDA_cublas_LIBRARY}   # Links to cublas

    cuda

    Threads::Threads
    m
    dl
)
