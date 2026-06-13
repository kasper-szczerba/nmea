cmake_minimum_required(VERSION 3.2)

# Set up project.
project(nmea
        VERSION 1.0
        DESCRIPTION "A library for NMEA 0183 messages.")

# Standard CMake module to define GNU standard installation directories (e.g., CMAKE_INSTALL_INCLUDEDIR)
include(GNUInstallDirs)

# Add source files.
file(GLOB_RECURSE sources ${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp)

# Create library.
add_library(nmea STATIC ${sources})

# Set include directories for internal/external use.
target_include_directories(nmea PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

# --- Installation Script Rules ---

# 1. Install the static library target
install(TARGETS nmea
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} # Typically 'lib'
)

# 2. Install the header files from your include directory
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}     # Typically 'include'
)