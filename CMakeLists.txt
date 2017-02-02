PROJECT(RAPP_CALIBRATE_CAMERA)

cmake_minimum_required(VERSION 2.8.3)

find_library(OPENCV_LIBRARIES NAMES opencv_highgui)
if (OPENCV_LIBRARIES)
    message(STATUS "found OpenCV")
elseif(!OPENCV_LIBRARIES)
    message(FATAL "missing OpenCV")
endif()

find_package(Rapp REQUIRED)
find_package(RappRobots REQUIRED)
find_package(Boost COMPONENTS system thread random REQUIRED)
find_package(Threads REQUIRED)

include_directories(${RAPP_INCLUDE_DIRS}/rapp)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${Rapp_DIR} ${RappRobots_DIR})
include(RappMacros)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++1y")

add_executable(learn_object main.cpp)

set(RAPP_LIBRARIES ${RAPP_LIBRARY} 
                   ${OPENSSL_LIBRARIES} 
		   ${Boost_LIBRARIES}
		   ${CMAKE_THREAD_LIBS_INIT})

target_link_libraries(learn_object ${RAPP_LIBRARIES} ${OPENCV_LIBRARIES})
