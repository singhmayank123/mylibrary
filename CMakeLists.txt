cmake_minimum_required(VERSION 3.15)
set(PACKAGE_VERSION 1.0.0)
project(mylibrary)
include(GNUInstallDirs)
include(CMakePackageConfigHelpers)
set(PORT_NAME mylibrary)
set(CONFIG_DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/${PORT_NAME}")
write_basic_package_version_file(
    MyLibConfigVersion.cmake
    VERSION ${PACKAGE_VERSION}
    COMPATIBILITY AnyNewerVersion
    )
add_library(mylibrary MyLibrary.cpp)
add_library(mylibrary::mylibrary ALIAS mylibrary)
configure_package_config_file(
    "${CMAKE_INSTALL_LIBDIR}/cmake/${PORT_NAME}-config.cmake.in"
    "${CMAKE_INSTALL_LIBDIR}/${PORT_NAME}-config.cmake"
    INSTALL_DESTINATION "${CONFIG_DESTINATION}"
)
install(
    TARGETS ${PORT_NAME}
    EXPORT ${PORT_NAME}-targets
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
)
