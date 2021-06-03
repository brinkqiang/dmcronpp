cmake_minimum_required(VERSION 3.2)

PROJECT(dmcronpp)

LIST(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
INCLUDE(cmake/ModuleImport.cmake)
INCLUDE(cmake/ModuleCompileOptions.cmake)
ModuleSetCompileOptions()

SET(DMCRONPP_VERSION_MAJOR "1")
SET(DMCRONPP_VERSION_MINOR "0")
SET(DMCRONPP_VERSION_PATCH "1")
SET(DMCRONPP_VERSION "${DMCRONPP_VERSION_MAJOR}.${DMCRONPP_VERSION_MINOR}.${DMCRONPP_VERSION_PATCH}")

MESSAGE(STATUS "VERSION: ${DMCRONPP_VERSION}")

OPTION(USE_DMCRONPP "use dmcronpp" OFF)
CONFIGURE_FILE(${CMAKE_CURRENT_SOURCE_DIR}/include/dmcronpp_config.h.in ${CMAKE_CURRENT_SOURCE_DIR}/include/dmcronpp_config.h)

LibImport("dmcronpp_module" "src/dmcronpp_module")
ExeImport("test" "dmcronpp_module")

#ADD_CUSTOM_COMMAND(
#TARGET dmcronpptest
#PRE_BUILD
#COMMAND ${CMAKE_COMMAND} -E copy_if_different
#${CMAKE_CURRENT_SOURCE_DIR}/config/test.csv
#$<TARGET_FILE_DIR:dmcronpptest>
#)

#INSTALL(DIRECTORY include/ DESTINATION include)
#INSTALL(TARGETS dmcronpp
#        RUNTIME DESTINATION bin
#        LIBRARY DESTINATION lib
#        ARCHIVE DESTINATION lib)

#SET(DMCRONPP_LIBS "dmcronpp")
#MARK_AS_ADVANCED(${DMCRONPP_LIBS})