set( DOXYGEN_EXAMPLE_LIST
  afterdoc
  author
  autolink
  class
  define
  docstring
  enum
  example
  file
  func
  group
  include
  jdstyle
  manual
  memgrp
  mux
  overload
  page
  par
  pyexample
  qtstyle
  relates
  restypedef
  structcmd
  tag
  templ
)

if( ${DOXYGEN_DOT_FOUND} )
  set( DOXYGEN_EXAMPLE_LIST
    ${DOXYGEN_EXAMPLE_LIST}
    diagrams
  )
endif()

set( DOXYGEN_TARGET_LIST )

foreach( e ${DOXYGEN_EXAMPLE_LIST} )
  set( _PROJECTNAME ${e} )
  set( _OUTPUTDIR ${CMAKE_CURRENT_BINARY_DIR}/${e} )
  set( _INPUTDIR  ${CMAKE_CURRENT_SOURCE_DIR} )
  set( _INPUT )

  if( EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/${e}.cpp )
    set( _INPUT ${CMAKE_CURRENT_SOURCE_DIR}/${e}.cpp )
  endif()

  if( EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/${e}.h )
    set( _INPUT ${_INPUT} ${CMAKE_CURRENT_SOURCE_DIR}/${e}.h )
  endif()

  if( EXISTS ${CMAKE_CURRENT_SOURCE_DIR}/${e}.py )
    set( _INPUT ${_INPUT} ${CMAKE_CURRENT_SOURCE_DIR}/${e}.py )
  endif()

  configure_file( ${CMAKE_SOURCE_DIR}/cmake/project.cfg.in
    ${CMAKE_CURRENT_BINARY_DIR}/${e}.cfg
    @ONLY
    )

  set( DOXYGEN_TARGET_LIST ${DOXYGEN_TARGET_LIST} DoxExample_${e} )

  add_custom_target( DoxExample_${e} ALL
    COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/${e}.cfg
    MAIN_DEPENDENCY ${CMAKE_CURRENT_BINARY_DIR}/${e}.cfg
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    )
endforeach()
