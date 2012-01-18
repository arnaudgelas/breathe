set( TINYXML_EXAMPLE_LIST
  tinyxml
)

foreach( e ${TINYXML_EXAMPLE_LIST} )
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
  add_custom_target( TinyXMLExample_${e} ALL
    COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_BINARY_DIR}/${e}.cfg
    MAIN_DEPENDENCY ${CMAKE_CURRENT_BINARY_DIR}/${e}.cfg
    WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
  )

endforeach()
