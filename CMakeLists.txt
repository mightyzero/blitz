cmake_minimum_required(VERSION 2.8)

project(blitz)

include_directories(./include /usr/local/)

set(srcfiles
    ./src/globals.cpp
)


set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")

add_library(blitz STATIC ${srcfiles})

add_subdirectory(test)

#-------------------------------------------------------#
# Add custom target, 'docs', to generate documentation. #
#-------------------------------------------------------#
find_package(Doxygen)
if (DOXYGEN_FOUND)
	# Set Doxygen output to the docs dir in the build directory
	set(DOCS_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/docs)

	# Generate Doxyfile from Doxyfile.in, plugging in CMake variables
	configure_file(
		${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in
		${CMAKE_BINARY_DIR}/Doxyfile @ONLY)

	# Add the make docs target
	add_custom_target(docs
		${DOXYGEN_EXECUTABLE} ${CMAKE_BINARY_DIR}/Doxyfile
		WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}
		COMMENT "Generating API documentation with Doxygen" VERBATIM)
endif (DOXYGEN_FOUND)
