cmake_minimum_required(VERSION 3.2)
project(MILD)
find_package(OpenCV 3 REQUIRED)
set(CMAKE_CXX_STANDARD 11)


if(UNIX)
set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build." FORCE)
set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR})
find_package( PkgConfig )
pkg_check_modules( EIGEN3 REQUIRED eigen3 )
include_directories( ${EIGEN3_INCLUDE_DIRS} )
set(CMAKE_CXX_FLAGS "-msse4.2") 
include_directories(${OpenCV_INCLUDE_DIRS})
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -Wall")
endif(UNIX)

if(MSVC)
	if(NOT DEFINED EIGEN3_INCLUDE_DIR)
		message("set EIGEN3_INCLUDE_DIR using -DEIGEN3_INCLUDE_DIR=... to build")
		return()
	endif()
include_directories(${EIGEN3_INCLUDE_DIR})
endif(MSVC)

file(GLOB helloworld_SRC
"*.cpp"
"*.h"
"MILD/*.cpp"
"MILD/*.h"
"ORBSLAM/*.cpp"
"ORBSLAM/*.h"
)


add_executable(MILD ${helloworld_SRC})
target_link_libraries(MILD ${OpenCV_LIBS} )
