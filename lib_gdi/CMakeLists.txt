# ==============================================================================
# SPDX short identifier: MPL-2.0
#
# CMakeList file for lib_gdi of dwservice-agent
# ==============================================================================

# ==============================================================================
# Dependencies
# ==============================================================================

find_package(PkgConfig REQUIRED)

pkg_check_modules(X11 REQUIRED IMPORTED_TARGET x11 xpm xft)

include_directories(${X11_INCLUDE_DIRS})

# ==============================================================================
# Library
# ==============================================================================

add_compile_options(-DOS_LINUX)

add_library(
  dwaggdi MODULE src/imagereader.cpp src/jsonwriter.cpp src/main.cpp src/main.h
                 src/linuxgdi.cpp
)

target_link_libraries(dwaggdi PUBLIC ${X11_LIBRARIES})

install(TARGETS dwaggdi DESTINATION dwagent/make/native)
