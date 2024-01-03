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

install(
    TARGETS ${PORT_NAME}
    EXPORT ${PORT_NAME}-targets
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
)

#install the targets files
install(
    EXPORT ${PORT_NAME}-targets
    NAMESPACE ${PORT_NAME}::
    DESTINATION "${CONFIG_DESTINATION}"
)
file(REMOVE_RECURSE
    ${CURRENT_PACKAGES_DIR}/debug/include
    ${CURRENT_PACKAGES_DIR}/debug/share
)

