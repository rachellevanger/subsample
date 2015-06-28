
cmake_minimum_required (VERSION 2.6) 
project (Subsample) 

set(CMAKE_MACOSX_RPATH 1)

# C++11 Support
if( CMAKE_COMPILER_IS_GNUCXX )
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -O3 -DNDEBUG")
else()
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -stdlib=libc++ -O3 -DNDEBUG")
endif()

add_definitions( -DINSTALLPREFIX="${MYPREFIX}" )

MESSAGE( STATUS "Chose the following prefix: " ${MYPREFIX} )

# Boost support
find_package(Boost 1.58.0 REQUIRED COMPONENTS system thread serialization chrono )

# OpenMPI
find_package(MPI REQUIRED)
include_directories(${MPI_INCLUDE_PATH})

include_directories( ./include /usr/local/include /opt/local/include ${Boost_INCLUDE_DIRS} ${USER_INCLUDE_PATH} )

link_directories( ${USER_LIBRARY_PATH} /usr/local/lib /opt/local/lib )


# Tell it where to put the products
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)


# Recurse into the "source" subdirectory.
add_subdirectory (source)

# Tests
# enable_testing()
# add_test( all ../tests/test.sh )
