find_package( Sphinx )

configure_file( ${CMAKE_CURRENT_SOURCE_DIR}/source/conf.py.in
  ${CMAKE_CURRENT_SOURCE_DIR}/source/conf.py
  @ONLY
  )

add_custom_target( html ALL
  COMMAND ${SPHINX_EXECUTABLE} -b html
  -P -a -d ${CMAKE_CURRENT_BINARY_DIR}/doctrees -D latex_paper_size=a4 ${CMAKE_CURRENT_SOURCE_DIR}/source
   ${CMAKE_CURRENT_BINARY_DIR}/html
  COMMENT "html pages are generated"
  )
