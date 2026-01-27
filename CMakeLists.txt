cmake_minimum_required(VERSION 3.20)

# Project info
project(mylib
    VERSION 0.1.0
    LANGUAGES CXX
)

# Flags
option(BUILD_TESTING   "Build tests"    ON)
option(BUILD_EXAMPLES  "Build examples" ON)

# Set main library
add_subdirectory(src)

# Tests
if (BUILD_TESTING)
    include(CTest)
    enable_testing()
    add_subdirectory(tests)
endif()

# Examples
if (BUILD_EXAMPLES)
    add_subdirectory(examples)
endif()


include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

# Installing the library itself
install(TARGETS mylib
    EXPORT mylibTargets
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

# Setting Headers
install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

# Exporting targets to a separate file
install(EXPORT mylibTargets
    NAMESPACE mylib::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mylib
    FILE mylibTargets.cmake
)

# Version file for find_package(mylib 0.1 CONFIG)
write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/mylibConfigVersion.cmake"
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY SameMajorVersion
)

# Config package
configure_package_config_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/mylibConfig.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/mylibConfig.cmake"
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mylib
)

# Installing configs
install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/mylibConfig.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/mylibConfigVersion.cmake"
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mylib
)