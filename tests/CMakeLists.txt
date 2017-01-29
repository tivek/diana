cmake_minimum_required(VERSION 3.0)

file(GLOB_RECURSE TEST_SOURCE "${CMAKE_CURRENT_SOURCE_DIR}/*.cpp")

add_executable(diana_test ${TEST_SOURCE})
#target_link_libraries(diana_test dianalib ${CONAN_LIBS})
target_link_libraries(diana_test ${CONAN_LIBS})
# We run our test from the source directory, so we can consistently
# load files with known paths.
# I also like color in my verbose output, so I put in a --force-colour flag.
add_test(NAME diana_test
         WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
         COMMAND ${CMAKE_BINARY_DIR}/bin/diana_test --force-colour)
