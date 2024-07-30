# ==============================================================================
# SPDX short identifier: MPL-2.0
#
# CMakeList file for `lib_soundcapture` of dwservice-agent
# ==============================================================================

# ==============================================================================
# Dependencies
# ==============================================================================

find_package(PkgConfig REQUIRED)

pkg_check_modules(RTAUDIO REQUIRED IMPORTED_TARGET rtaudio)
pkg_check_modules(OPUS REQUIRED IMPORTED_TARGET opus)

# ==============================================================================
# dwagsoundcapture
# ==============================================================================

include_directories(${RTAUDIO_INCLUDE_DIRS} ${OPUS_INCLUDE_DIRS})

add_library(dwagsoundcapture MODULE src/main.cpp src/common/logger.cpp)
target_link_libraries(dwagsoundcapture ${RTAUDIO_LIBRARIES} ${OPUS_LIBRARIES})

install(TARGETS dwagsoundcapture DESTINATION dwagent/make/native)

install(FILES config.json DESTINATION dwagent/lib_soundcapture)
