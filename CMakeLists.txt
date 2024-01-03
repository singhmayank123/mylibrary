cmake_minimum_required(VERSION 3.15)
set(PACKAGE_VERSION 1.0.0)
project(mylibrary)
include(GNUInstallDirs)
include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    MyLibConfigVersion.cmake
    VERSION ${PACKAGE_VERSION}
    COMPATIBILITY AnyNewerVersion
    )
add_library(mylibrary MyLibrary.cpp)
add_library(mylibrary::mylibrary ALIAS mylibrary)

install(TARGETS MyLib
   EXPORT MyLibTargets
   LIBRARY DESTINATION lib
   ARCHIVE DESTINATION lib
   RUNTIME DESTINATION bin
   INCLUDES DESTINATION include
)

install(EXPORT MyLibTargets
        FILE MyLibTargets.cmake
        NAMESPACE MyLib::
        DESTINATION cmake
         )

