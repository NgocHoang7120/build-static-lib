cmake_minimum_required(VERSION 3.22.1)
project("iamf")

add_subdirectory(opus)
add_subdirectory(aac)
add_library(libopus STATIC IMPORTED)
set_target_properties(
        libopus PROPERTIES
        IMPORTED_LOCATION "${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}/libopus.a"
)

add_library(${CMAKE_PROJECT_NAME}
        SHARED
        # List C/C++ source files with relative paths to this CMakeLists.txt.
        native-lib.cpp)
#include header file from opus folder
target_include_directories(${CMAKE_PROJECT_NAME} PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}/opus/include
)

find_library(
        lib-log
        log
)

if(TARGET libopus)
    target_link_libraries(${CMAKE_PROJECT_NAME} PUBLIC ${libopus})
else()
    message(WARNING "libopus is not defined. Make sure to define it.")
endif()

target_link_libraries(${CMAKE_PROJECT_NAME}
        # List libraries link to the target library
        ${libopus}
        android
        ${lib-log}
)