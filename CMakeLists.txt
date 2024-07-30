# ==============================================================================
# SPDX short identifier: MPL-2.0
#
# Top-level CMake file for DWService - Agent
# ==============================================================================

cmake_minimum_required(VERSION 3.26)

project(dwagent C CXX)

# ==============================================================================
# Options
# ==============================================================================

set(CMAKE_EXPORT_COMPILE_COMMANDS On)

option(UI_SUPPORT "Install UI component" On)
option(APP_DESKTOP "Install Desktop application" On)
option(APP_FILE_SYSTEM "Install FileSystem application" On)
option(APP_LOG_WATCH "Install LogWatch application" On)
option(APP_RESOURCE "Install Resource application" On)
option(APP_TEXT_EDITOR "Install Text Editor application" On)

# ==============================================================================
# Native Libraries
# ==============================================================================

set(CMAKE_SHARED_MODULE_PREFIX_CXX
    ""
    CACHE STRING "Remove `lib` prefix from libraries"
)
add_subdirectory(lib_core)
add_subdirectory(lib_gdi)
add_subdirectory(lib_osutil)
add_subdirectory(lib_screencapture)
add_subdirectory(lib_soundcapture)

# ==============================================================================
# INSTALL
# ==============================================================================

#
# Libraries / Native
#

install(FILES lib_z/config.json DESTINATION dwagent/lib_z)
install(FILES lib_rtaudio/config.json DESTINATION dwagent/lib_rtaudio)
install(FILES lib_opus/config.json DESTINATION dwagent/lib_opus)
install(FILES lib_turbojpeg/config.json DESTINATION dwagent/lib_turbojpeg)
install(FILES lib_stdcpp/config.json DESTINATION dwagent/lib_stdcpp)

install(FILES make/create_config.py make/detectinfo.py make/utils.py
        DESTINATION dwagent/make
)

#
# Core
#

install(
  DIRECTORY core
  DESTINATION dwagent
  PATTERN "mytest*" EXCLUDE
  PATTERN ".*project" EXCLUDE
)

install(
  DIRECTORY os_linux
  DESTINATION dwagent
  PATTERN "mytest*" EXCLUDE
  PATTERN ".*" EXCLUDE
)

#
# UI
#

install(
  DIRECTORY ui
  DESTINATION dwagent
  PATTERN "mytest*" EXCLUDE
  PATTERN ".*" EXCLUDE
)

#
# APPS
#

if(APP_DESKTOP)
  install(
    DIRECTORY app_desktop
    DESTINATION dwagent
    PATTERN "mytest*" EXCLUDE
    PATTERN ".*" EXCLUDE
  )
endif()

if(APP_FILE_SYSTEM)
  install(
    DIRECTORY app_filesystem
    DESTINATION dwagent
    PATTERN "mytest*" EXCLUDE
    PATTERN ".*" EXCLUDE
  )
endif()

if(APP_LOG_WATCH)
  install(
    DIRECTORY app_logwatch
    DESTINATION dwagent
    PATTERN "mytest*" EXCLUDE
    PATTERN ".*" EXCLUDE
  )
endif()

if(APP_RESOURCE)
  install(
    DIRECTORY app_resource
    DESTINATION dwagent
    PATTERN "mytest*" EXCLUDE
    PATTERN ".*" EXCLUDE
  )
endif()

if(APP_SHELL)
  install(
    DIRECTORY app_shell
    DESTINATION dwagent
    PATTERN "mytest*" EXCLUDE
    PATTERN ".*" EXCLUDE
  )
endif()

if(APP_TEXT_EDITOR)
  install(
    DIRECTORY app_texteditor
    DESTINATION dwagent
    PATTERN "mytest*" EXCLUDE
    PATTERN ".*" EXCLUDE
  )
endif()
