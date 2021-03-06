# Copyright (C) 2008-2010 Trinity <http://www.trinitycore.org/>
#
# This file is free software; as a special exception the author gives
# unlimited permission to copy and/or distribute it, with or without
# modifications, as long as this notice is preserved.
#
# This program is distributed in the hope that it will be useful, but
# WITHOUT ANY WARRANTY, to the extent permitted by law; without even the
# implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

set(sources
    IntermediateValues.cpp
    IntermediateValues.h
    MapBuilder.cpp
    MapBuilder.h
    PathCommon.h
    PathGenerator.cpp
    TerrainBuilder.cpp
    TerrainBuilder.h
    VMapExtensions.cpp
)

# definitions
add_definitions(-DNO_CORE_FUNCS)
add_definitions(-DDEBUG)
add_definitions(-DNO_vsnprintf)

include_directories(
  ${ACE_INCLUDE_DIR}
  ${MYSQL_INCLUDE_DIR}
  ${CMAKE_SOURCE_DIR}/dep/libmpq
  ${CMAKE_SOURCE_DIR}/dep/zlib
  ${CMAKE_SOURCE_DIR}/dep/acelite
  ${CMAKE_SOURCE_DIR}/dep/mysqllite/include/internal
  ${CMAKE_SOURCE_DIR}/dep/include/g3dlite
  ${CMAKE_SOURCE_DIR}/dep/recastnavigation/Recast
  ${CMAKE_SOURCE_DIR}/dep/recastnavigation/Detour
  ${CMAKE_SOURCE_DIR}/src/shared
  ${CMAKE_SOURCE_DIR}/src/shared/Database
  ${CMAKE_SOURCE_DIR}/src/collision
  ${CMAKE_SOURCE_DIR}/src/framework
  ${CMAKE_SOURCE_DIR}/src/game
)

add_executable(movements_extractor
    ${sources}
)

target_link_libraries(movements_extractor
  ${MYSQL_LIBRARY}
  ${ACE_LIBRARY}
  ${BZIP2_LIBRARIES}
  ${ZLIB_LIBRARIES}
  Recast
  Detour
  collision
  g3dlite
  shared
  oregonframework
)

if( UNIX )
  install(TARGETS movements_extractor DESTINATION bin)
elseif( WIN32 )
  install(TARGETS movements_extractor DESTINATION "${CMAKE_INSTALL_PREFIX}")
endif()