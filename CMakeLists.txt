cmake_minimum_required(VERSION 3.16)

project(parsefshTest LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(FILE_PATH "data/USERDATA.ADM")

add_executable(parsefsh
  src/splitimg.cpp
  src/admfunc.h
)

add_executable(parsetrk
  src/parsetrk.cpp
  src/admfunc.h
)

include(GNUInstallDirs)
install(TARGETS parsefsh
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)

add_custom_command(
    OUTPUT
        ${CMAKE_CURRENT_BINARY_DIR}/${FILE_PATH}
    DEPENDS
        ${CMAKE_CURRENT_SOURCE_DIR}/${FILE_PATH}
    COMMAND
        ${CMAKE_COMMAND} -E copy_if_different
        ${CMAKE_CURRENT_SOURCE_DIR}/${FILE_PATH}
        ${CMAKE_CURRENT_BINARY_DIR}/${FILE_PATH}
)
add_custom_target(copy DEPENDS ${CMAKE_CURRENT_BINARY_DIR}/${FILE_PATH})
