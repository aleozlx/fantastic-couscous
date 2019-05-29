cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
# list(APPEND CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/cmake/modules)

if(${CMAKE_VERSION} VERSION_LESS "3.8.0")
    project(superpixel-analyzer)
else()
    project(superpixel-analyzer LANGUAGES CXX)
    # project(superpixel-analyzer LANGUAGES CXX CUDA)
    # https://stackoverflow.com/questions/53859271/cmake-cannot-find-cuda-could-not-find-cmake-module-file-cmakedeterminecudacom
endif()

find_package(OpenCV REQUIRED)
# find_package(VTK REQUIRED)
# find_package(TensorFlow REQUIRED)
# find_package(CUDA 10 REQUIRED)
# find_package(Boost)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()
set(CMAKE_CXX_FLAGS_DEBUG "-g")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${SSE_FLAGS} -march=native -fopenmp")
# set(CMAKE_EXE_LINKER_FLAGS  "${CMAKE_EXE_LINKER_FLAGS} -fPIC --shared -D_GLIBCXX_USE_CXX11_ABI=${TensorFlow_ABI}" )

include_directories(SYSTEM ${OpenCV_INCLUDE_DIRS})
add_executable(superpixel-analyzer "main.cc")
target_link_libraries(superpixel-analyzer
    opencv_core
    opencv_highgui
    opencv_imgproc
    opencv_ximgproc
    opencv_videoio
    opencv_video
    opencv_imgcodecs
)
