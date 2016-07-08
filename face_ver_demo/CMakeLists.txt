cmake_minimum_required (VERSION 2.8.11)
project (face_ver_demo)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")

add_library(dlib SHARED IMPORTED)   # Dynamic import
set_target_properties(dlib PROPERTIES IMPORTED_LOCATION ${CMAKE_SOURCE_DIR}/../lib/libdlib.so)
include(../dlib/cmake)  

find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})
find_package(Boost REQUIRED)
find_package(Boost COMPONENTS filesystem system REQUIRED)
include_directories(${Boost_INCLUDE_DIRS})
find_package(HDF5 REQUIRED)
include_directories(${HDF5_INCLUDE_DIRS})
#find_package(Flann REQUIRED)
#include_directories(${FLANN_INCLUDE_DIRS})

include_directories("../include")
link_directories("../lib")
set(FaceRecSrzn_LIBRARIES "face_rec_srzn;caffe;dlib")

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
add_executable(face_ver face_ver_demo.cpp )
target_link_libraries(face_ver ${FaceRecSrzn_LIBRARIES} ${OpenCV_LIBRARIES} ${Boost_LIBRARIES} )
