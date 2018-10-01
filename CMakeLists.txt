cmake_minimum_required(VERSION 3.2)

project(homework_1 VERSION 0.0.$ENV{TRAVIS_BUILD_NUMBER})

configure_file(version.h.in version.h)

add_executable(hw1_cli main.cpp)

add_library(LibFunctions lib.cpp)

add_executable(LibFunctionsTests_cli test_main.cpp)

target_link_libraries(hw1_cli LibFunctions)
