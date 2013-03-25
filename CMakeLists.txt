cmake_minimum_required( VERSION 2.8 )
project( libnoise )

set( CMAKE_BUILD_TYPE Release CACHE STRING "Build Type." FORCE )
set( LIBNOISE_BUILD_SHARED_LIBS FALSE CACHE BOOL "Build shared libraries." )
set( LIBNOISE_BUILD_DOC FALSE CACHE BOOL "Build Doxygen documentation." )

set( LIBNOISE_INCLUDE_DIR_NAME "noise" CACHE STRING "Define the name of the include directory for libnoise." )
set( LIBNOISE_SKIP_INSTALL FALSE CACHE BOOL "Don't install libnoise." )
mark_as_advanced( LIBNOISE_INCLUDE_DIR_NAME )
mark_as_advanced( LIBNOISE_SKIP_INSTALL )

if( LIBNOISE_BUILD_SHARED_LIBS )
	set( LIB_TYPE SHARED )
else()
	set( LIB_TYPE STATIC )
endif()

set( SRC_DIR "src" )
set( INC_DIR "include" )

set(
	SOURCES
	${INC_DIR}/noise/basictypes.h
	${INC_DIR}/noise/exception.h
	${INC_DIR}/noise/interp.h
	${INC_DIR}/noise/latlon.h
	${INC_DIR}/noise/mathconsts.h
	${INC_DIR}/noise/misc.h
	${INC_DIR}/noise/noise.h
	${INC_DIR}/noise/noisegen.h
	${INC_DIR}/noise/vectortable.h
	${INC_DIR}/noise/model/cylinder.h
	${INC_DIR}/noise/model/line.h
	${INC_DIR}/noise/model/model.h
	${INC_DIR}/noise/model/plane.h
	${INC_DIR}/noise/model/sphere.h
	${INC_DIR}/noise/module/abs.h
	${INC_DIR}/noise/module/add.h
	${INC_DIR}/noise/module/billow.h
	${INC_DIR}/noise/module/blend.h
	${INC_DIR}/noise/module/cache.h
	${INC_DIR}/noise/module/checkerboard.h
	${INC_DIR}/noise/module/clamp.h
	${INC_DIR}/noise/module/const.h
	${INC_DIR}/noise/module/curve.h
	${INC_DIR}/noise/module/cylinders.h
	${INC_DIR}/noise/module/displace.h
	${INC_DIR}/noise/module/exponent.h
	${INC_DIR}/noise/module/invert.h
	${INC_DIR}/noise/module/max.h
	${INC_DIR}/noise/module/min.h
	${INC_DIR}/noise/module/module.h
	${INC_DIR}/noise/module/modulebase.h
	${INC_DIR}/noise/module/multiply.h
	${INC_DIR}/noise/module/perlin.h
	${INC_DIR}/noise/module/power.h
	${INC_DIR}/noise/module/ridgedmulti.h
	${INC_DIR}/noise/module/rotatepoint.h
	${INC_DIR}/noise/module/scalebias.h
	${INC_DIR}/noise/module/scalepoint.h
	${INC_DIR}/noise/module/select.h
	${INC_DIR}/noise/module/spheres.h
	${INC_DIR}/noise/module/terrace.h
	${INC_DIR}/noise/module/translatepoint.h
	${INC_DIR}/noise/module/turbulence.h
	${INC_DIR}/noise/module/voronoi.h
	${SRC_DIR}/latlon.cpp
	${SRC_DIR}/noisegen.cpp
	${SRC_DIR}/model/cylinder.cpp
	${SRC_DIR}/model/line.cpp
	${SRC_DIR}/model/plane.cpp
	${SRC_DIR}/model/sphere.cpp
	${SRC_DIR}/module/abs.cpp
	${SRC_DIR}/module/add.cpp
	${SRC_DIR}/module/billow.cpp
	${SRC_DIR}/module/blend.cpp
	${SRC_DIR}/module/cache.cpp
	${SRC_DIR}/module/checkerboard.cpp
	${SRC_DIR}/module/clamp.cpp
	${SRC_DIR}/module/const.cpp
	${SRC_DIR}/module/curve.cpp
	${SRC_DIR}/module/cylinders.cpp
	${SRC_DIR}/module/displace.cpp
	${SRC_DIR}/module/exponent.cpp
	${SRC_DIR}/module/invert.cpp
	${SRC_DIR}/module/max.cpp
	${SRC_DIR}/module/min.cpp
	${SRC_DIR}/module/modulebase.cpp
	${SRC_DIR}/module/multiply.cpp
	${SRC_DIR}/module/perlin.cpp
	${SRC_DIR}/module/power.cpp
	${SRC_DIR}/module/ridgedmulti.cpp
	${SRC_DIR}/module/rotatepoint.cpp
	${SRC_DIR}/module/scalebias.cpp
	${SRC_DIR}/module/scalepoint.cpp
	${SRC_DIR}/module/select.cpp
	${SRC_DIR}/module/spheres.cpp
	${SRC_DIR}/module/terrace.cpp
	${SRC_DIR}/module/translatepoint.cpp
	${SRC_DIR}/module/turbulence.cpp
	${SRC_DIR}/module/voronoi.cpp
)

include_directories( ${INC_DIR}/noise )

add_library( libnoise ${LIB_TYPE} ${SOURCES} )

# GCC will automatically add the prefix lib
if( CMAKE_COMPILER_IS_GNUCXX )
	set_target_properties( libnoise PROPERTIES OUTPUT_NAME noise )
endif()

if(LIBNOISE_BUILD_DOC)
	add_subdirectory( doc )
endif()

if( NOT LIBNOISE_SKIP_INSTALL )
	install(
		TARGETS libnoise
		RUNTIME DESTINATION bin COMPONENT bin
		LIBRARY DESTINATION lib COMPONENT bin
		ARCHIVE DESTINATION lib COMPONENT dev
	)

	install(
		DIRECTORY include/noise/
		DESTINATION include/${LIBNOISE_INCLUDE_DIR_NAME}
	)
endif()