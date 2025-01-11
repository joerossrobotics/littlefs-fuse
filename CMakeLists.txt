cmake_minimum_required(VERSION 3.28.0)

project(littlefs_fuse)

# Compiler flags
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -pedantic -D_FILE_OFFSET_BITS=64 -D_XOPEN_SOURCE=700 -DLFS_MULTIVERSION -DLFS_MIGRATE")

add_library(littlefs STATIC
    "littlefs/lfs.c"
    "littlefs/lfs_util.c"
)

target_include_directories(littlefs PUBLIC
    "littlefs"
)

add_executable(littlefs_fuse
    "lfs_fuse.c"
    "lfs_fuse_bd.c"
)

target_link_libraries(littlefs_fuse littlefs fuse)

install(TARGETS littlefs_fuse
    RUNTIME DESTINATION bin
)
