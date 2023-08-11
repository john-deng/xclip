cmake_minimum_required(VERSION 3.13)
project(xclip VERSION 0.13 LANGUAGES C)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}")

find_package(X11 REQUIRED)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -g -O2 -Wall")
add_definitions(
        -DPACKAGE_NAME="xclip"
        -DPACKAGE_TARNAME="xclip"
        -DPACKAGE_VERSION="0.13"
        -DPACKAGE_STRING="xclip 0.13"
        -DPACKAGE_BUGREPORT=""
        -DPACKAGE_URL=""
        -DSTDC_HEADERS=1
        -DHAVE_SYS_TYPES_H=1
        -DHAVE_SYS_STAT_H=1
        -DHAVE_STDLIB_H=1
        -DHAVE_STRING_H=1
        -DHAVE_MEMORY_H=1
        -DHAVE_STRINGS_H=1
        -DHAVE_INTTYPES_H=1
        -DHAVE_STDINT_H=1
        -DHAVE_UNISTD_H=1
        -DHAVE_ICONV=1
        -DHAVE_LIBXMU=1
)

add_executable(xclip
        xclib.c
        xcprint.c
        xclip.c
        )

target_link_libraries(xclip PRIVATE X11::X11 X11::Xmu)

install(
        TARGETS xclip
        RUNTIME DESTINATION bin
)

install(
        FILES xclip-copyfile xclip-pastefile xclip-cutfile
        PERMISSIONS OWNER_READ OWNER_WRITE OWNER_EXECUTE GROUP_READ GROUP_EXECUTE WORLD_READ WORLD_EXECUTE
        DESTINATION bin
)

install(
        FILES xclip.1 xclip-copyfile.1
        PERMISSIONS OWNER_READ OWNER_WRITE GROUP_READ WORLD_READ
        DESTINATION share/man/man1
)

