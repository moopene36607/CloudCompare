
option( PLUGIN_IO_QE57 "Install qE57_IO plugin to read & write E57 files using libE57Format" OFF )

if ( PLUGIN_IO_QE57 )
	project( QE57_IO_PLUGIN )

	include( CMakePolicies NO_POLICY_SCOPE )

	set( CC_IS_IO_PLUGIN 1 )

	include_directories( extern/libE57Format/include )
	include_directories( src )

	add_subdirectory( src )
	add_subdirectory( extern/libE57Format EXCLUDE_FROM_ALL )
	
	include( ../../../CMakePluginTpl.cmake )
	
	target_link_libraries( ${PROJECT_NAME} E57Format )
	
	if ( USING_STATIC_XERCES )
		target_compile_definitions( ${PROJECT_NAME} PRIVATE XERCES_STATIC_LIBRARY )
    endif()	
endif()
