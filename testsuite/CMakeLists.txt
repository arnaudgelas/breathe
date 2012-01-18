find_package( Sphinx )

add_custom_target( copy_sources ALL
  COMMAND ${CMAKE_COMMAND} -E copy_directory
  "${CMAKE_CURRENT_SOURCE_DIR}/source"
  "${CMAKE_CURRENT_BINARY_DIR}/source"
  COMMENT "Copying sources"
  )

configure_file( ${CMAKE_CURRENT_SOURCE_DIR}/source/conf.py.in
  ${CMAKE_CURRENT_BINARY_DIR}/source/conf.py
  @ONLY
  )

add_custom_target( html ALL
  COMMAND ${SPHINX_EXECUTABLE} -b html
  -P -a -d ${CMAKE_CURRENT_BINARY_DIR}/doctrees -D latex_paper_size=a4 ${CMAKE_CURRENT_BINARY_DIR}/source
   ${CMAKE_CURRENT_BINARY_DIR}/html
  DEPENDS ${DOXYGEN_TARGET_LIST} ${SPECIFIC_TARGET_LIST} ${TINYXML_TARGET_LIST}
  COMMENT "html pages are generated"
  )
