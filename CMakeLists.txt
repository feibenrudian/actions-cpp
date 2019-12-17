cmake_minimum_required(VERSION 3.10)
# TODO: named this project here
project(money)

set(CMAKE_CXX_STANDARD 17)

message("DEBUG XXX: ${CMAKE_MODULE_PATH}")
#set(CMAKE_MODULE_PATH ${CMAKE_BINARY_DIR} ${CMAKE_MODULE_PATH})

#include(${CMAKE_SOURCE_DIR}/conanbuildinfo.cmake)
#conan_basic_setup()

find_package(GTest REQUIRED)

aux_source_directory(src ALL_SOURCES)

set(SOURCES ${ALL_SOURCES})
list(FILTER SOURCES EXCLUDE REGEX "^.*Test.cpp$")
add_executable(${PROJECT_NAME} ${SOURCES})

set(TEST_SOURCES ${ALL_SOURCES})
list(FILTER TEST_SOURCES INCLUDE REGEX "^.*Test.cpp$")
if(NOT "${TEST_SOURCES}" STREQUAL "")
    add_executable(${PROJECT_NAME}_test ${TEST_SOURCES})
    target_link_libraries(${PROJECT_NAME}_test gtest::gtest)
    enable_testing()
    add_test(NAME test COMMAND ${PROJECT_NAME}_test)
endif()
