cmake_minimum_required(VERSION 3.15)
set(mylibrary_VERSION 1.0.0)
project(mylibrary)
add_library(mylibrary MyLibrary.cpp)
add_library(mylibrary::mylibrary ALIAS mylibrary)

 

