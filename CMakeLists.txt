cmake_minimum_required(VERSION 3.2)

project(homework VERSION 0.0.$ENV{TRAVIS_BUILD_NUMBER})

find_package(Boost COMPONENTS unit_test_framework REQUIRED)

configure_file(version.h.in version.h)

add_executable(homework_cli main.cpp)

add_library(LibFunctions lib.cpp)

add_executable(LibFunctionsTests_cli test_main.cpp)

set_target_properties(homework_cli LibFunctionsTests_cli PROPERTIES
	CXX_STANDARD 14
	CXX_STANDARD_REQUIRED ON
	COMPILE_OPTIONS -Wpedantic -Wall -Wextra
)

set_target_properties(LibFunctionsTests_cli PROPERTIES
	COMPILE_DEFINITIONS BOOST_TEST_DYN_LINK
	INCLUDE_DIRECTORIES ${Boost_INCLUDE_DIR}
)

target_link_libraries(homework_cli LibFunctions)

target_link_libraries(LibFunctionsTests_cli
	LibFunctions
	${Boost_LIBRARIES}
)

enable_testing()

install(TARGETS homework_cli RUNTIME DESTINATION bin)

set(CPACK_GENERATOR DEB)

set(CPACK_PACKAGE_VERSION_MAJOR "${PROJECT_VERSION_MAJOR}")
set(CPACK_PACKAGE_VERSION_MINOR "${PROJECT_VERSION_MINOR}")
set(CPACK_PACKAGE_VERSION_PATCH "${PROJECT_VERSION_PATCH}")

set(CPACK_PACKAGE_CONTACT leon8005@gmail.com)

set(CPACK_DEBIAN_PACKAGE_SHLIBDEPS ON)

include(CPack)

add_test(VersionNum_IsGreaterThanZero LibFunctionsTests_cli)
