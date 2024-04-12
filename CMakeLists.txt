cmake_minimum_required(VERSION 3.10)

project(libgif)

# Set target library name
set(TARGET_NAME libgif)

# Set minimum required SDK version
# CMake doesn't directly use SDK versions, but you can store it for reference
set(CMAKE_ANDROID_SDK_VERSION 9)

# Source files
set(SOURCE_FILES
  dgif_lib.c
  egif_lib.c
  gifalloc.c
  gif_err.c
  gif_hash.c
  openbsd-reallocarray.c
  quantize.c
)

# Compiler flags
set(CMAKE_C_FLAGS "-Werror")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-format")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-sign-compare")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wno-unused-parameter")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DHAVE_CONFIG_H")

# Include directories
include_directories(".")

# Add static library
add_library(${TARGET_NAME} SHARED ${SOURCE_FILES})

# Make library available for linking by other projects
set_target_properties(${TARGET_NAME} PROPERTIES POSITION_INDEPENDENT_CODE ON)

# remove library prefix
set_target_properties(libgif PROPERTIES PREFIX "")