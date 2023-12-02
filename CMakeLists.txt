cmake_minimum_required(VERSION 3.24) # CMakePresets are supported since version 3.21

project(cpp_proj_template
        VERSION 0.1.0
        LANGUAGES CXX)

# Make all modules available to this project and other projects that consume this project by
# adding the cmake directory to the CMAKE_MODULE_PATH
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_LIST_DIR}/cmake)
include(warnings)
include(static_analysis)

# Set common properties for cross platform builds
include(project_preamble)
project_preamble()

if ((CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR))
    set(IS_TOP_LEVEL_PROJECT TRUE)
else ()
    set(IS_TOP_LEVEL_PROJECT FALSE)
endif ()

if (IS_TOP_LEVEL_PROJECT)
    option(${PROJECT_NAME}_USE_SCCACHE "Use sccache" ON)
    option(${PROJECT_NAME}_USE_WARNINGS "Compile using warnings." ON)
    option(${PROJECT_NAME}_WARNINGS_AS_ERRORS "Treat compiler warnings as errors " ON)
    option(${PROJECT_NAME}_STATIC_ANALYSIS "" ON)
else ()
    option(${PROJECT_NAME}_USE_SCCACHE "Use sccache" OFF)
    option(${PROJECT_NAME}_USE_WARNINGS "Compile using warnings." OFF)
    option(${PROJECT_NAME}_WARNINGS_AS_ERRORS "Treat compiler warnings as errors" OFF)
    option(${PROJECT_NAME}_STATIC_ANALYSIS "" OFF)
endif ()

if (${PROJECT_NAME}_USE_SCCACHE)
    include(setup_sccache)
    enable_sccache()
endif ()

# Use find_package to find dependencies that are installed on the system
# Example:
# find_package(Boost REQUIRED)


