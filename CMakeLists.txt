cmake_minimum_required(VERSION 2.8)
project (crow_sample)

find_package(Threads)

if (NOT CMAKE_BUILD_TYPE)
    message(STATUS "No build type selected, default to Release")
    set(CMAKE_BUILD_TYPE "Release")
endif()


if (MSVC)
set(Boost_USE_STATIC_LIBS "On")
find_package( Boost 1.52 COMPONENTS date_time filesystem system thread regex REQUIRED )
else()
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -std=c++1y")
find_package( Boost 1.52 COMPONENTS date_time filesystem system thread REQUIRED )
endif()

include_directories( ${Boost_INCLUDE_DIR} )

set(PROJECT_INCLUDE_DIR
${PROJECT_SOURCE_DIR}/include
)

include_directories("${PROJECT_INCLUDE_DIR}")
include_directories("${PROJECT_SOURCE_DIR}")

add_executable(main main.cpp)
target_link_libraries(main ${Boost_LIBRARIES})
target_link_libraries(main ${CMAKE_THREAD_LIBS_INIT})