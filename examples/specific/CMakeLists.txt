set( SPECIFIC_EXAMPLE_LIST
  alias
  nutshell
  c_file
  rst
  class
  template_class
  fixedwidthfont
  template_class_non_type
  inline
  template_function
  members
  typedef
  multifile
  userdefined
  namespacefile
)

set( SPECIFIC_TARGET_LIST )

foreach( e ${SPECIFIC_EXAMPLE_LIST} )
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

  configure_file( ${CMAKE_SOURCE_DIR}/cmake/project.cfg.in
    ${CMAKE_CURRENT_BINARY_DIR}/${e}.cfg
    @ONLY
  )
  set( SPECIFIC_TARGET_LIST ${SPECIFIC_TARGET_LIST} SpecificExample_${e} )

  add_custom_target( SpecificExample_${e} ALL
    COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/${e}.cfg
    MAIN_DEPENDENCY ${CMAKE_CURRENT_BINARY_DIR}/${e}.cfg
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
  )

endforeach()
