cmake_minimum_required(VERSION 3.2)

project(homework_1 VERSION 0.0.$ENV{TRAVIS_BUILD_NUMBER})

find_package(Boost COMPONENTS unit_test_framework REQUIRED)

configure_file(version.h.in version.h)

add_executable(hw1_cli main.cpp)

add_library(LibFunctions lib.cpp)

add_executable(LibFunctionsTests_cli test_main.cpp)

target_link_libraries(hw1_cli LibFunctions)

set_target_properties(LibFunctionsTests_cli PROPERTIES
	COMPILE_DEFINITIONS BOOST_TEST_DYN_LINK
	INCLUDE_DIRECTORIES ${Boost_INCLUDE_DIR}
)

