cmake_minimum_required(VERSION 4.0)
project(C_Template C)

set(CMAKE_C_STANDARD 23)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -g")

if(CMAKE_VERSION VERSION_LESS 4.0)
    message(FATAL_ERROR "Required CMake 4.0+")
endif()

file(GLOB SOURCES "src/*.c")

add_executable(${PROJECT_NAME} ${SOURCES})
