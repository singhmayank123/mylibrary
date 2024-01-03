cmake_minimum_required(VERSION 3.15)
set(mylibrary_VERSION 1.0.0)
project(mylibrary)
add_library(mylibrary MyLibrary.cpp)
add_library(mylibrary::mylibrary ALIAS mylibrary)
install(TARGETS MyLib
        EXPORT MyLibTargets
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        RUNTIME DESTINATION bin
        INCLUDES DESTINATION include
        )

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    MyLibConfigVersion.cmake
    VERSION ${PACKAGE_VERSION}
    COMPATIBILITY AnyNewerVersion
    )

 

