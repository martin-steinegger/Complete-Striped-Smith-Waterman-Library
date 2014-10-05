cmake_minimum_required(VERSION 2.4)
project (MMseqs)
set(sampleName MMseqs)

set(MMSEQS_DIR ${PROJECT_SOURCE_DIR})
set(CMAKE_LIBRARY_PATH ${CMAKE_LIBRARY_PATH} ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_VERBOSE_MAKEFILE ON)
message("-- Sourcedir ${CMAKE_CURRENT_SOURCE_DIR}")
message("-- Projjectdir ${PROJECT_SOURCE_DIR}")
# find compiler
if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  # using Clang
  message("-- Compilter is clang(++)")
  set(CMAKE_COMPILER_IS_CLANG 1)
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  # using GCC
  message("-- Compilter is GNU ")
  set(CMAKE_COMPILER_IS_GNUCXX 1)
  set(CMAKE_COMPILER_IS_GNUCCC 1)
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Intel")
  # using Intel C++
  set(CMAKE_COMPILER_IS_ICC 1)
endif()

#zlib
find_package( ZLIB REQUIRED )
#math
find_library(M_LIB m)

#SSE
SET (CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
INCLUDE(CheckSSEFeatures)
ADD_DEFINITIONS(${CXX_DFLAGS})

# set flags
set(CMAKE_CXX_FLAGS                "${CMAKE_CXX_FLAGS} -Wall -Wno-write-strings -std=c++11 -m64")
set(CMAKE_CXX_FLAGS_DEBUG          "${CMAKE_CXX_FLAGS_DEBUG} -O0 -g ")
set(CMAKE_CXX_FLAGS_MINSIZEREL     "${CMAKE_CXX_FLAGS_MINSIZEREL} -Os -DNDEBUG")
set(CMAKE_CXX_FLAGS_RELEASE        "${CMAKE_CXX_FLAGS_RELEASE} -O3 -DNDEBUG -ffast-math -ftree-vectorize -fno-strict-aliasing -Wno-write-stringse")
set(CMAKE_CXX_FLAGS_RELWITHDEBINFO "${CMAKE_CXX_FLAGS_RELWITHDBINFO} -O2 -g")
set(CMAKE_XCODE_ATTRIBUTE_CLANG_CXX_LANGUAGE_STANDARD "c++11")
set(CMAKE_XCODE_ATTRIBUTE_CLANG_CXX_LIBRARY "libc++")

#set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GCC_COMPILE_FLAGS}” )
include_directories(src)
add_subdirectory(src)
