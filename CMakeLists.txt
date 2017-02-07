cmake_minimum_required(VERSION 3.0)
find_package(OpenCL REQUIRED)

set(CLINFO_SOURCES src/error.h
    src/ext.h
    src/fmtmacros.h
    src/memory.h
    src/ms_support.h
    src/strbuf.h
    src/clinfo.c)

# DL_INCLUDE_PATH and DL_LIBRARY point to the directory containing dlcfn.h, and to a .lib file for dl-related functions, respectively.
# On Windows, you must find/create these yourself; on Linux, DL_INCLUDE_PATH can be blank, and DL_LIBRARY can be "-ldl"
# TODO: Use more idoimatic CMake for finding and setting these variables

add_executable(clinfo ${CLINFO_SOURCES})
target_include_directories(clinfo PRIVATE ${OpenCL_INCLUDE_DIRS} ${DL_INCLUDE_PATH})
target_link_libraries(clinfo PRIVATE ${OpenCL_LIBRARIES} ${DL_LIBRARY})
