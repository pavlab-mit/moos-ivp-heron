#########################################################################
# FILE:        moos-ivp-heron/src/CMakeLists.txt
# DATE:        Mar 30, 2025
# DESCRIPTION: CMakeLists.txt file for the moos-ivp-heron source directory
#########################################################################


#========================================================================
# Add the libraries in the current directory to the include path
#========================================================================
FILE(GLOB LOCAL_LIBRARY_DIRS ./lib_*)
INCLUDE_DIRECTORIES(${LOCAL_LIBRARY_DIRS})

#========================================================================
# Let users control whether or not GUI-related libraries/apps are built.
#========================================================================
SET(BUILD_BOT_CODE_ONLY OFF CACHE BOOL "Build minimal set of bot apps.")

#===============================================================
# Set the ROBOT Apps
#===============================================================

SET(ROBOT_APPS)

IF( EXISTS ${CMAKE_SOURCE_DIR}/src/lib_sock_utils )
  LIST(APPEND ROBOT_APPS lib_sock_utils)
ENDIF()

IF( EXISTS ${CMAKE_SOURCE_DIR}/src/iM300 )
  LIST(APPEND ROBOT_APPS iM300)
ENDIF()

IF( EXISTS ${CMAKE_SOURCE_DIR}/src/iM300Health )
  LIST(APPEND ROBOT_APPS iM300Health)
ENDIF()

SET(APPS_TO_BUILD ${ROBOT_APPS})
FOREACH(A ${APPS_TO_BUILD})
  message("APP:" ${A})
  ADD_SUBDIRECTORY(${A})
ENDFOREACH(A)

#########################################################################
#                           END of CMakeLists.txt
#########################################################################

