cmake_minimum_required(VERSION 3.15)
# TODO: named this project here
project()

set(CMAKE_CXX_STANDARD 17)

include(${CMAKE_SOURCE_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

aux_source_directory(src ALL_SOURCES)

set(SOURCES ${ALL_SOURCES})
list(FILTER SOURCES EXCLUDE REGEX "^.*Test.cpp$")
add_executable(${PROJECT_NAME} ${SOURCES})

set(TEST_SOURCES ${ALL_SOURCES})
list(FILTER TEST_SOURCES INCLUDE REGEX "^.*Test.cpp$")
if(NOT "${TEST_SOURCES}" STREQUAL "")
    add_executable(${PROJECT_NAME}_test ${TEST_SOURCES})
    target_link_libraries(${PROJECT_NAME}_test ${CONAN_LIBS})
    enable_testing()
    add_test(NAME test COMMAND ${PROJECT_NAME}_test)
endif()
