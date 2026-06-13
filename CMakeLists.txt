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

# Generate and install package config files for CMake find_package()
include(CMakePackageConfigHelpers)

write_basic_package_version_file(
    ${CMAKE_CURRENT_BINARY_DIR}/nmeaConfigVersion.cmake
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY AnyNewerVersion
)

configure_package_config_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/nmeaConfig.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/nmeaConfig.cmake
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/nmea
)

# --- Installation Script Rules ---

# 1. Install the static library target
install(TARGETS nmea
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} # Typically 'lib'
)

# 2. Install the header files from your include directory
install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}     # Typically 'include'
)