# ==============================================================================
# SPDX short identifier: MPL-2.0
#
# CMakeList file for `osutil` of dwservice-agent
# ==============================================================================

# ==============================================================================
# dwascreencapture
# ==============================================================================

add_library(dwagosutil MODULE src/main.cpp src/jsonwriter.cpp src/util.cpp)

target_link_libraries(dwagosutil PUBLIC dl)

install(TARGETS dwagosutil DESTINATION dwagent/make/native)

install(FILES config.json DESTINATION dwagent/lib_osutil)
