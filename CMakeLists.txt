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
	${INC_DIR}/${PROJECT_NAME}/basictypes.h
	${INC_DIR}/${PROJECT_NAME}/exception.h
	${INC_DIR}/${PROJECT_NAME}/interp.h
	${INC_DIR}/${PROJECT_NAME}/latlon.h
	${INC_DIR}/${PROJECT_NAME}/mathconsts.h
	${INC_DIR}/${PROJECT_NAME}/misc.h
	${INC_DIR}/${PROJECT_NAME}/noise.h
	${INC_DIR}/${PROJECT_NAME}/noisegen.h
	${INC_DIR}/${PROJECT_NAME}/vectortable.h
	${INC_DIR}/${PROJECT_NAME}/model/cylinder.h
	${INC_DIR}/${PROJECT_NAME}/model/line.h
	${INC_DIR}/${PROJECT_NAME}/model/model.h
	${INC_DIR}/${PROJECT_NAME}/model/plane.h
	${INC_DIR}/${PROJECT_NAME}/model/sphere.h
	${INC_DIR}/${PROJECT_NAME}/module/abs.h
	${INC_DIR}/${PROJECT_NAME}/module/add.h
	${INC_DIR}/${PROJECT_NAME}/module/billow.h
	${INC_DIR}/${PROJECT_NAME}/module/blend.h
	${INC_DIR}/${PROJECT_NAME}/module/cache.h
	${INC_DIR}/${PROJECT_NAME}/module/checkerboard.h
	${INC_DIR}/${PROJECT_NAME}/module/clamp.h
	${INC_DIR}/${PROJECT_NAME}/module/const.h
	${INC_DIR}/${PROJECT_NAME}/module/curve.h
	${INC_DIR}/${PROJECT_NAME}/module/cylinders.h
	${INC_DIR}/${PROJECT_NAME}/module/displace.h
	${INC_DIR}/${PROJECT_NAME}/module/exponent.h
	${INC_DIR}/${PROJECT_NAME}/module/invert.h
	${INC_DIR}/${PROJECT_NAME}/module/max.h
	${INC_DIR}/${PROJECT_NAME}/module/min.h
	${INC_DIR}/${PROJECT_NAME}/module/module.h
	${INC_DIR}/${PROJECT_NAME}/module/modulebase.h
	${INC_DIR}/${PROJECT_NAME}/module/multiply.h
	${INC_DIR}/${PROJECT_NAME}/module/perlin.h
	${INC_DIR}/${PROJECT_NAME}/module/power.h
	${INC_DIR}/${PROJECT_NAME}/module/ridgedmulti.h
	${INC_DIR}/${PROJECT_NAME}/module/rotatepoint.h
	${INC_DIR}/${PROJECT_NAME}/module/scalebias.h
	${INC_DIR}/${PROJECT_NAME}/module/scalepoint.h
	${INC_DIR}/${PROJECT_NAME}/module/select.h
	${INC_DIR}/${PROJECT_NAME}/module/spheres.h
	${INC_DIR}/${PROJECT_NAME}/module/terrace.h
	${INC_DIR}/${PROJECT_NAME}/module/translatepoint.h
	${INC_DIR}/${PROJECT_NAME}/module/turbulence.h
	${INC_DIR}/${PROJECT_NAME}/module/voronoi.h
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

include_directories( ${INC_DIR}/${PROJECT_NAME} )

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