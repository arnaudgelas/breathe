cmake_minimum_required(VERSION 2.8)

project( breathe )

set( CMAKE_MODULE_PATH
  ${CMAKE_SOURCE_DIR}/cmake
  ${CMAKE_MODULE_PATH}
)

include( ${CMAKE_ROOT}/Modules/Documentation.cmake )

add_subdirectory( testsuite )

add_subdirectory( examples )

add_subdirectory( breathe )
