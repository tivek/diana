project(diana)
cmake_minimum_required(VERSION 3.0)

# C++17 because we're "edgy".
set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} "-std=c++1z")

# Setup conan and include everything.
include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

# Include the src directory, so we can freely include our headers from there.
include_directories(src)
# Grab all *.cpp files recursively.
file(GLOB_RECURSE PROJECT_SOURCE 
"${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")

# Exclude main file for library generation, only use it in the final
# executable. This lets us test everything without compiling twice.
set(PROJECT_MAIN "${CMAKE_CURRENT_SOURCE_DIR}/src/main.cpp")
list(REMOVE_ITEM PROJECT_SOURCE ${PROJECT_MAIN})

# Build our project with the help of conan.
include_directories(${CONAN_INCLUDE_DIRS})
#add_library(dianalib STATIC ${PROJECT_SOURCE})
add_executable(diana ${PROJECT_MAIN})
#target_link_libraries(diana dianalib ${CONAN_LIBS})
target_link_libraries(diana ${CONAN_LIBS})

# Now enable our tests.
enable_testing()
add_subdirectory(tests)
