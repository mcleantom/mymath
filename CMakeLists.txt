cmake_minimum_required(VERSION 3.5)
project(mymath)

add_library(mymath SHARED mymath.cpp)

target_include_directories(mymath PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
