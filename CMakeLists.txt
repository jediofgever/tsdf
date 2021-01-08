cmake_minimum_required (VERSION 3.15)

project(diana)

option(USE_CUDA "Use CUDA" ON)

file(GLOB cpu_source_files "*.hpp")
file(GLOB gpu_source_files "*.cu")
SET(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS};-O3 -gencode arch=compute_50,code=sm_50)
set(CUDA_TOOLKIT_ROOT_DIR "/usr/local/cuda")

# OpenCV
find_package(OpenCV 4 REQUIRED)
find_package(CUDA 11 REQUIRED)

message(STATUS "Use cuda ${CUDA_VERSION}")
message(STATUS "Use OpenCV ${OpenCV_VERSION}")
message(STATUS "Use Cmake ${CMAKE_VERSION}")

include_directories(${OpenCV_INCLUDE_DIRS}
                    ${CUDA_INCLUDE_DIRS})

CUDA_ADD_EXECUTABLE(diana ${cpu_source_files} ${gpu_source_files})
target_link_libraries(diana ${OpenCV_LIBRARIES} ${CUDA_LIBRARIES})

 