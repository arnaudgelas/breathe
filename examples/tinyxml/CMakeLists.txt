set( TINYXML_EXAMPLE_LIST
  tinyxml
)

foreach( e ${DOXYGEN_EXAMPLE_LIST} )
  add_custom_target( DoxExample_${e} ALL
    COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/${e}.cfg
    MAIN_DEPENDENCY ${e}.cfg
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    )
endforeach()
