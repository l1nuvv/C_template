# CMake minimum version
cmake_minimum_required(VERSION 4.0)
project(C_Template C)

# Enforce CMake version
if (CMAKE_VERSION VERSION_LESS 4.0)
  message(FATAL_ERROR "CMake 4.0 or higher is required.")
endif ()

# Language and standard
set(CMAKE_C_STANDARD 23)
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

# Build type default
if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Build type (Debug, Release)" FORCE)
endif ()

# Compiler flags
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -g")
set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -O0")
set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -O3 -s")

# Output directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin")

# Include directories
include_directories(${PROJECT_SOURCE_DIR}/include)

# Timestamp
string(TIMESTAMP TODAY "%Y-%m-%d")
string(TIMESTAMP NOW "%H:%M:%S")

# Clang-format support
find_program(CLANG_FORMAT "clang-format")
if (CLANG_FORMAT)
  add_custom_target(
          format
          COMMAND ${CLANG_FORMAT} -i src/*.c include/*.h
          COMMENT "Formatting C code"
  )
endif ()

# Configuration info
message(STATUS "Project: ${PROJECT_NAME}")
message(STATUS "Build Type: ${CMAKE_BUILD_TYPE}")
message(STATUS "C Compiler: ${CMAKE_C_COMPILER}")
message(STATUS "C Standard: C${CMAKE_C_STANDARD}")
message(STATUS "Configuration completed")
message(STATUS "Date: ${TODAY}")
message(STATUS "Time: ${NOW}")

# Source files
file(GLOB SOURCES "src/*.c")

# Executable target
add_executable(${PROJECT_NAME} ${SOURCES})
