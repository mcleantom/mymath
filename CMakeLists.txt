cmake_minimum_required(VERSION 3.10)
project(mymath VERSION 1.0.0)

# Add the library
add_library(mymath STATIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>/mymath.cpp)

# Include directories
target_include_directories(mymath PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
    $<INSTALL_INTERFACE:include>
)

get_target_property(MYMATH_PUBLIC_HEADERS mymath INTERFACE_SOURCES)
set_target_properties(mylib PROPERTIES PUBLIC_HEADER "${MYLIB_PUBLIC_HEADERS}")

# Specify installation rules
install(TARGETS mymath
    EXPORT mymathTargets
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin
    PUBLIC_HEADER DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}/mylib"
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
