cmake_minimum_required(VERSION 3.15)

set(mylibrary_VERSION 1.0.0)

project(mylibrary
    VERSION ${mylibrary_VERSION}
    DESCRIPTION "Your description here"
    HOMEPAGE_URL "https://github.com/singhmayank123/mylibrary"
    LANGUAGES CXX)

include(CMakePackageConfigHelpers)
include(GNUInstallDirs)

add_library(mylibrary src/mylibrary.cpp include/mylibrary.h)
add_library(mylibrary::mylibrary ALIAS mylibrary)

if(BUILD_SHARED_LIBS AND WIN32)
    target_compile_definitions(mylibrary
        PRIVATE "MYLIBRARY_EXPORT=__declspec(dllexport)"
        INTERFACE "MYLIBRARY_EXPORT=__declspec(dllimport)")
endif()

target_compile_features(mylibrary PUBLIC cxx_std_17)
target_include_directories(mylibrary
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>)

configure_package_config_file(cmake/config.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/mylibrary-config.cmake
    INSTALL_DESTINATION ${CMAKE_INSTALL_DATADIR}/mylibrary
    NO_SET_AND_CHECK_MACRO)
write_basic_package_version_file(
    ${CMAKE_CURRENT_BINARY_DIR}/mylibrary-config-version.cmake
    VERSION ${mylibrary_VERSION}
    COMPATIBILITY SameMajorVersion)

install(
    FILES
        ${CMAKE_CURRENT_BINARY_DIR}/mylibrary-config.cmake
        ${CMAKE_CURRENT_BINARY_DIR}/mylibrary-config-version.cmake
    DESTINATION
        ${CMAKE_INSTALL_DATADIR}/mylibrary)

install(TARGETS mylibrary EXPORT mylibrary-targets)
install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})
install(EXPORT mylibrary-targets
    NAMESPACE mylibrary::
    DESTINATION ${CMAKE_INSTALL_DATADIR}/mylibrary)
