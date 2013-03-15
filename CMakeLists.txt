cmake_minimum_required( VERSION 2.8 )
project( libnoise )

set( LIBNOISE_BUILD_SHARED_LIB FALSE CACHE BOOL "Build shared libraries." )
set( CMAKE_BUILD_TYPE Release CACHE STRING "Build Type." FORCE)

if( LIBNOISE_BUILD_SHARED_LIB )
	set( LIB_TYPE SHARED )
else()
	set( LIB_TYPE STATIC )
endif()

set( SRC_DIR "src" )
set( INC_DIR "include" )

set(
	SOURCES
	${INC_DIR}/libnoise/basictypes.h
	${INC_DIR}/libnoise/exception.h
	${INC_DIR}/libnoise/interp.h
	${INC_DIR}/libnoise/latlon.h
	${INC_DIR}/libnoise/mathconsts.h
	${INC_DIR}/libnoise/misc.h
	${INC_DIR}/libnoise/noise.h
	${INC_DIR}/libnoise/noisegen.h
	${INC_DIR}/libnoise/vectortable.h
	${INC_DIR}/libnoise/model/cylinder.h
	${INC_DIR}/libnoise/model/line.h
	${INC_DIR}/libnoise/model/model.h
	${INC_DIR}/libnoise/model/plane.h
	${INC_DIR}/libnoise/model/sphere.h
	${INC_DIR}/libnoise/module/abs.h
	${INC_DIR}/libnoise/module/add.h
	${INC_DIR}/libnoise/module/billow.h
	${INC_DIR}/libnoise/module/blend.h
	${INC_DIR}/libnoise/module/cache.h
	${INC_DIR}/libnoise/module/checkerboard.h
	${INC_DIR}/libnoise/module/clamp.h
	${INC_DIR}/libnoise/module/const.h
	${INC_DIR}/libnoise/module/curve.h
	${INC_DIR}/libnoise/module/cylinders.h
	${INC_DIR}/libnoise/module/displace.h
	${INC_DIR}/libnoise/module/exponent.h
	${INC_DIR}/libnoise/module/invert.h
	${INC_DIR}/libnoise/module/max.h
	${INC_DIR}/libnoise/module/min.h
	${INC_DIR}/libnoise/module/module.h
	${INC_DIR}/libnoise/module/modulebase.h
	${INC_DIR}/libnoise/module/multiply.h
	${INC_DIR}/libnoise/module/perlin.h
	${INC_DIR}/libnoise/module/power.h
	${INC_DIR}/libnoise/module/ridgedmulti.h
	${INC_DIR}/libnoise/module/rotatepoint.h
	${INC_DIR}/libnoise/module/scalebias.h
	${INC_DIR}/libnoise/module/scalepoint.h
	${INC_DIR}/libnoise/module/select.h
	${INC_DIR}/libnoise/module/spheres.h
	${INC_DIR}/libnoise/module/terrace.h
	${INC_DIR}/libnoise/module/translatepoint.h
	${INC_DIR}/libnoise/module/turbulence.h
	${INC_DIR}/libnoise/module/voronoi.h
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

include_directories( ${INC_DIR} )

add_library( libnoise ${LIB_TYPE} ${SOURCES} )

# GCC will automatically add the prefix lib
if( CMAKE_COMPILER_IS_GNUCXX )
	set_target_properties( libnoise PROPERTIES OUTPUT_NAME noise )
endif()

if( NOT NOISE_SKIP_INSTALL )
	install(
		TARGETS libnoise
		RUNTIME DESTINATION bin COMPONENT bin
		LIBRARY DESTINATION lib COMPONENT bin
		ARCHIVE DESTINATION lib COMPONENT dev
	)

	install(
		DIRECTORY include/libnoise
		DESTINATION include
	)
endif()