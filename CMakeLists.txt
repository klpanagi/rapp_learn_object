PROJECT(RAPP_CALIBRATE_CAMERA)

cmake_minimum_required(VERSION 2.8.3)

find_package(Rapp REQUIRED)
find_package(RappRobots REQUIRED)
find_package(Boost COMPONENTS system thread random REQUIRED)
find_package(Threads REQUIRED)

find_library(OPENCV NAMES opencv_highgui HINTS /usr/lib /usr/local/lib)

include_directories(${RAPP_INCLUDE_DIRS}/rapp)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${Rapp_DIR} ${RappRobots_DIR})
include(RappMacros)

setup_rapp()
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++1y")

add_executable(LearnObject main.cpp)

set(RAPP_LIBRARIES ${RAPP_LIBRARY} 
                   ${OPENSSL_LIBRARIES} 
		   ${Boost_LIBRARIES}
		   ${CMAKE_THREAD_LIBS_INIT})

target_link_libraries(object_recognition ${RAPP_LIBRARIES}
                                         ${OPENCV})
