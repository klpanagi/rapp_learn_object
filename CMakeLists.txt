PROJECT(RAPP_CALIBRATE_CAMERA)

cmake_minimum_required(VERSION 2.8.3)

find_package(OpenCV REQUIRED)
find_package(Rapp REQUIRED)
find_package(RappRobots REQUIRED)
find_package(Boost COMPONENTS system thread random REQUIRED)
find_package(Threads REQUIRED)

	       
find_library(RAPP_ROBOT_COMMUNICATION NAMES rapp_robot_communication)
find_library(RAPP_ROBOT_INFO NAMES rapp_robot_info) 
find_library(RAPP_ROBOT_LOCALIZATION NAMES rapp_robot_localization)
find_library(RAPP_ROBOT_NAVIGATION NAMES rapp_robot_navigation)
find_library(RAPP_ROBOT_VISION NAMES rapp_robot_vision)

find_library(RAPP_LIBRARY NAMES rapp REQUIRED)

include_directories(${RAPP_INCLUDE_DIRS}/rapp)

message(STATUS "libraries: ${RAPP_LIBRARY}")

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${Rapp_DIR} ${RappRobots_DIR})
include(RappMacros)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=gnu++1y")

add_executable(learn_object main.cpp)

set(RAPP_LIBRARIES ${RAPP_LIBRARY}
	           ${RAPP_ROBOT_COMMUNICATION}
		   ${RAPP_ROBOT_INFO}
		   ${RAPP_ROBOT_LOCALIZATION}
		   ${RAPP_ROBOT_NAVIGATION}
		   ${RAPP_ROBOT_VISION}
                   ${OPENSSL_LIBRARIES} 
		   ${Boost_LIBRARIES}
		   ${CMAKE_THREAD_LIBS_INIT})

target_link_libraries(learn_object ${RAPP_LIBRARIES} ${OpenCV_LIBS})
