# SPDX-License-Identifier: BSD-3-Clause
# Copyright Contributors to the OpenColorIO Project.

set(SOURCES
    main.cpp
)

add_executable(ociocheck ${SOURCES})

if(MSVC)
    set(PLATFORM_COMPILE_OPTIONS "${PLATFORM_COMPILE_OPTIONS};/wd4996")
endif()

set_target_properties(ociocheck PROPERTIES 
    COMPILE_OPTIONS "${PLATFORM_COMPILE_OPTIONS}"
    LINK_OPTIONS "${PLATFORM_LINK_OPTIONS}"
)

target_link_libraries(ociocheck 
    PRIVATE 
        apputils
        OpenColorIO
)

include(StripUtils)
ocio_strip_binary(ociocheck)

install(TARGETS ociocheck
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
