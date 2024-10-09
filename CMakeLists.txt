cmake_minimum_required(VERSION 3.10)
project(mymath VERSION 1.0.0)

# Add the header and source files
add_library(mymath STATIC mymath.cpp mymath.h)

# Optionally add include directories if needed
target_include_directories(mymath PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# Install rules
install(TARGETS mymath
        EXPORT mymathTargets
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        RUNTIME DESTINATION bin)

install(EXPORT mymathTargets
        FILE mymathTargets.cmake
        NAMESPACE mymath::
        DESTINATION lib/cmake/mymath)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/
        DESTINATION include
        FILES_MATCHING PATTERN "*.h")
