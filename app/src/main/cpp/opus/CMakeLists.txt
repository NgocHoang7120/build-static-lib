set(INCLUDE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/include")
#include này được sử dụng trên toàn bộ dự án thường đứng ở cmakelists root
#include_directories(INCLUDE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/include")

message(WARNING "INCLUDE_PATH = ${INCLUDE_PATH}")

set(LIBRARY_OUTPUT_PATH "${CMAKE_SOURCE_DIR}/libs/${ANDROID_ABI}")
message(WARNING "LIBRARY_OUTPUT_PATH = ${LIBRARY_OUTPUT_PATH}")

file(MAKE_DIRECTORY ${LIBRARY_OUTPUT_PATH})

add_library(
        opus
        STATIC
        src/test.cpp
)

# set output file .a
set_target_properties(
        opus PROPERTIES
        ARCHIVE_OUTPUT_DIRECTORY ${LIBRARY_OUTPUT_PATH}
)

target_include_directories(
        opus PUBLIC
        ${INCLUDE_PATH}
)


