set(PROJECT_NAME envi)

set(CMAKE_BUILD_TYPE Debug)

#set(CMAKE_LEGACY_CYGWIN_WIN32 0) # Remove when CMake >= 2.8.4 is required
cmake_minimum_required(VERSION 3.0)
project(${PROJECT_NAME})

Option(BUILD_GPROF "Build for Profiling" OFF)
if (BUILD_GPROF)
message("Profiling")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pg -Wall -pedantic -std=c++0x -U__STRICT_ANSI__ -Wno-invalid-offsetof")
else ()
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pedantic -std=c++0x -U__STRICT_ANSI__ -Wno-invalid-offsetof")
endif ()

IF(${CMAKE_SYSTEM_NAME} MATCHES "Linux")
    # Linux specific code
    SET(OperatingSystem "Linux")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")
	if (${CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT})
		set(CMAKE_INSTALL_PREFIX "$ENV{HOME}" CACHE PATH "default install path" FORCE )
	endif()

ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Linux")

IF(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
   # Windows 7 specific code
   SET(OperatingSystem "Windows 7")
ENDIF(${CMAKE_SYSTEM_NAME} MATCHES "Windows")

set(LIBRARIES_SOURCE "$ENV{LIBRARIES_SOURCE}")

add_subdirectory(${PROJECT_SOURCE_DIR}/libraries ${CMAKE_BINARY_DIR}/libraries)
#add_subdirectory(${PROJECT_SOURCE_DIR}/programs ${CMAKE_BINARY_DIR}/programs)
