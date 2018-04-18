cmake_minimum_required(VERSION 3.5.1)

# add the binary tree directory to the search path 
# for include files
include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/src ${CMAKE_CURRENT_SOURCE_DIR}/.. )
 
SET(SRCS
    ${CMAKE_CURRENT_SOURCE_DIR}/src/nanovg.c
    ${CMAKE_CURRENT_SOURCE_DIR}/../android_file.cpp
    )

SET(HDRS
    ${CMAKE_CURRENT_SOURCE_DIR}/../android_file.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/fontstash.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/nanovg.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/nanovg_gl.h 
    ${CMAKE_CURRENT_SOURCE_DIR}/src/nanovg_gl_utils.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/stb_image.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/stb_truetype.h
    )

# add the main library
if(BUILD_SHARED_LIBS)
  add_library(nanovg SHARED ${SRCS} ${HDRS})
  install (TARGETS nanovg DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()

if(BUILD_STATIC_LIBS)
  add_library(nanovg-static STATIC ${SRCS} ${HDRS})
  install (TARGETS nanovg-static DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
 
install (FILES ${HDRS} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

foreach(p LIB INCLUDE)
    set(var CMAKE_INSTALL_${p}DIR)
    if(NOT IS_ABSOLUTE "${${var}}")
        set(${var} "${CMAKE_INSTALL_PREFIX}/${${var}}")
    endif()
endforeach()
