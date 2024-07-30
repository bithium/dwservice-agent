# ==============================================================================
# SPDX short identifier: MPL-2.0
#
# CMakeList file for dwaglib of dwservice-agent
# ==============================================================================

add_library(dwaglib MODULE src/main.cpp src/main.h)

target_sources(dwaglib PRIVATE src/linux.cpp)
target_compile_definitions(dwaglib PRIVATE -DOS_LINUX)
target_link_libraries(dwaglib pthread rt)

install(TARGETS dwaglib DESTINATION dwagent/make/native)
