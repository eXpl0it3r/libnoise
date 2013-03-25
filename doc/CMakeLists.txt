# Create Doxygen documentation
find_package( Doxygen REQUIRED )

set( LIBNOISE_INPUT_DOXYFILE "${CMAKE_SOURCE_DIR}/doc/Doxyfile" )
set( LIBNOISE_OUTPUT_DOXYFILE "${CMAKE_BINARY_DIR}/doc/Doxyfile" )

# Copy doxyfile, replacing only @variables@
configure_file( ${LIBNOISE_INPUT_DOXYFILE} ${LIBNOISE_OUTPUT_DOXYFILE} @ONLY )

# Add target for documentation, invokes Doxygen
add_custom_target(
	doc ALL
	COMMAND ${DOXYGEN_EXECUTABLE} "${CMAKE_BINARY_DIR}/doc/Doxyfile"
	WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/doc/
	)

# Install documentation to doc directory
if( NOT LIBNOISE_SKIP_INSTALL )
	install(
			DIRECTORY ${CMAKE_BINARY_DIR}/doc/html/
			DESTINATION doc
			COMPONENT doc
			)
endif()