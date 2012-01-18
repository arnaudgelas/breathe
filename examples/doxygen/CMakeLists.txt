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

foreach( e ${DOXYGEN_EXAMPLE_LIST} )
  add_custom_target( DoxExample_${e} ALL
    COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/${e}.cfg
    MAIN_DEPENDENCY ${e}.cfg
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    )
endforeach()
