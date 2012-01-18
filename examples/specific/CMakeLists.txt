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

foreach( e ${SPECIFIC_EXAMPLE_LIST} )
  add_custom_target( SpecificExample_${e} ALL
    COMMAND ${DOXYGEN_EXECUTABLE} ${CMAKE_CURRENT_SOURCE_DIR}/${e}.cfg
    MAIN_DEPENDENCY ${e}.cfg
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    )
endforeach()
