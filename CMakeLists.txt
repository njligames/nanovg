cmake_minimum_required(VERSION 3.7)

# add the binary tree directory to the search path 
# for include files
include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/src )
 
SET(SRCS
    ${CMAKE_CURRENT_SOURCE_DIR}/src/nanovg.c
    )

SET(HDRS
    ${CMAKE_CURRENT_SOURCE_DIR}/src/fontstash.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/nanovg.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/nanovg_gl.h 
    ${CMAKE_CURRENT_SOURCE_DIR}/src/nanovg_gl_utils.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/stb_image.h
    ${CMAKE_CURRENT_SOURCE_DIR}/src/stb_truetype.h
    )

# add the main library
add_library(nanovg SHARED ${SRCS} ${HDRS})
add_library(nanovg ${SRCS} ${HDRS})
 
install (TARGETS nanovg DESTINATION ${CMAKE_INSTALL_LIBDIR})
install (FILES ${HDRS} DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

foreach(p LIB INCLUDE)
    set(var CMAKE_INSTALL_${p}DIR)
    if(NOT IS_ABSOLUTE "${${var}}")
        set(${var} "${CMAKE_INSTALL_PREFIX}/${${var}}")
    endif()
endforeach()
