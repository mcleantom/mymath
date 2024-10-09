cmake_minimum_required(VERSION 3.10)
project(mymath VERSION 1.0.0)

# Add the library
add_library(mymath STATIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>/mymath.cpp)

# Include directories
target_include_directories(mymath PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include>
)

# Specify installation rules
install(TARGETS mymath
    EXPORT mymathTargets
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
)

install(EXPORT mymathTargets
    FILE mymathTargets.cmake
    NAMESPACE mymath::
    DESTINATION share/cmake/mymath
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/
    DESTINATION include
    FILES_MATCHING PATTERN "*.h"
)

install(
    EXPORT mymathTargets
    DESTINATION share/mymath
    FILE mymathConfig.cmake
)
