cmake_minimum_required(VERSION 2.6)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pedantic -std=c++11 -U__STRICT_ANSI__ -Wno-invalid-offsetof")

include_directories(${CMAKE_CURRENT_SOURCE_DIR})
#include_directories(${COSMOS_HOME}/include)
include_directories(${MY_INCLUDES})

FILE(GLOB SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
FILE(GLOB INCLUDES ${CMAKE_CURRENT_SOURCE_DIR}/*.h)

get_filename_component(LIB_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)

add_library(envi STATIC ${SOURCES} ${INCLUDES})

install(TARGETS envi DESTINATION lib)
install(FILES ${INCLUDES} DESTINATION include)
