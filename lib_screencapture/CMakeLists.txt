# ==============================================================================
# SPDX short identifier: MPL-2.0
#
# CMakeList file for `dwascreencapture` of dwservice-agent
# ==============================================================================

# ==============================================================================
# Dependencies
# ==============================================================================

find_package(PkgConfig REQUIRED)

pkg_check_modules(ZLIB REQUIRED IMPORTED_TARGET zlib)
pkg_check_modules(TURBOJPEG REQUIRED IMPORTED_TARGET libturbojpeg)
pkg_check_modules(
  X11
  REQUIRED
  IMPORTED_TARGET
  x11
  xext
  xtst
  xdamage
  xfixes
)

include_directories(
  ${ZLIB_INCLUDE_DIRS} ${TURBOJPEG_INCLUDE_DIRS} ${X11_INCLUDE_DIRS}
)

# ==============================================================================
# dwascreencapture
# ==============================================================================

add_compile_options(-DOS_MAIN -DOS_LINUX -DOS_XORG)

add_library(
  dwagscreencapture MODULE
  src/main.cpp
  src/common/logger.cpp
  src/common/timecounter.cpp
  src/common/util.cpp
  src/linux/linuxcpuusage.cpp
  src/linux/linuxinputsxorg.cpp
  src/linux/linuxkeysym2ucs.cpp
)

target_link_libraries(
  dwagscreencapture PUBLIC ${ZLIB_LIBRARIES} ${TURBOJPEG_LIBRARIES}
                           ${X11_LIBRARIES} dl
)

install(TARGETS dwagscreencapture DESTINATION dwagent/make/native)

install(FILES config.json DESTINATION dwagent/lib_screencapture)

# ==============================================================================
# dwascreencapturexorg
# ==============================================================================

add_library(dwagscreencapturexorg MODULE src/xorg/screencapturenativexorg.cpp)

target_link_libraries(dwagscreencapturexorg PUBLIC ${X11_LIBRARIES} dl)
install(TARGETS dwagscreencapturexorg DESTINATION dwagent/make/native)
