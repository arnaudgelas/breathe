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

set( DOXYGEN_TARGET_LIST )

if( ${DOXYGEN_DOT_FOUND} )
  set( _PROJECTNAME diagrams )
  set( _OUTPUTDIR ${CMAKE_CURRENT_BINARY_DIR}/${_PROJECTNAME} )
  set( _INPUTDIR  ${CMAKE_CURRENT_SOURCE_DIR} )

  set( _INPUT " \"${CMAKE_CURRENT_SOURCE_DIR}/diagrams_a.h \\ \n \"" )
  set( _INPUT "\" ${_INPUT} ${CMAKE_CURRENT_SOURCE_DIR}/diagrams_b.h \\ \n \"" )
  set( _INPUT "\" ${_INPUT} ${CMAKE_CURRENT_SOURCE_DIR}/diagrams_c.h \\ \n \"" )
  set( _INPUT "\" ${_INPUT} ${CMAKE_CURRENT_SOURCE_DIR}/diagrams_d.h \\ \n \"" )
  set( _INPUT "\" ${_INPUT} ${CMAKE_CURRENT_SOURCE_DIR}/diagrams_e.h \"" )

  configure_file( ${CMAKE_SOURCE_DIR}/cmake/project.cfg.in
    ${CMAKE_CURRENT_BINARY_DIR}/${_PROJECTNAME}.cfg
    @ONLY
    )

  set( DOXYGEN_TARGET_LIST ${DOXYGEN_TARGET_LIST} DoxExample_${_PROJECTNAME} )

  add_custom_target( DoxExample_${_PROJECTNAME} ALL
    COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/${_PROJECTNAME}.cfg
    MAIN_DEPENDENCY ${CMAKE_CURRENT_BINARY_DIR}/${_PROJECTNAME}.cfg
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
    )
endif()

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
