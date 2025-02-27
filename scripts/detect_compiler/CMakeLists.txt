cmake_minimum_required(VERSION 3.20)
project(detect_compiler NONE)

if(CMAKE_GENERATOR STREQUAL "Ninja" AND CMAKE_SYSTEM_NAME STREQUAL "Windows")
    set(CMAKE_C_COMPILER_WORKS 1)
    set(CMAKE_C_COMPILER_FORCED 1)
    set(CMAKE_CXX_COMPILER_WORKS 1)
    set(CMAKE_CXX_COMPILER_FORCED 1)
endif()

enable_language(C)
enable_language(CXX)
if(APPLE)
    enable_language(OBJC)
    enable_language(OBJCXX)
endif()

file(SHA1 "${CMAKE_CXX_COMPILER}" CXX_HASH)
file(SHA1 "${CMAKE_C_COMPILER}" C_HASH)
set(OBJC_HASH "")
set(OBJCXX_HASH "")
if(APPLE)
    file(SHA1 "${CMAKE_OBJC_COMPILER}" OBJC_HASH)
    file(SHA1 "${CMAKE_OBJCXX_COMPILER}" OBJCXX_HASH)
endif()
string(SHA1 COMPILER_HASH "${C_HASH}${CXX_HASH}${OBJC_HASH}${OBJCXX_HASH}")


message("#COMPILER_HASH#${COMPILER_HASH}")
message("#COMPILER_C_HASH#${C_HASH}")
message("#COMPILER_C_VERSION#${CMAKE_C_COMPILER_VERSION}")
message("#COMPILER_C_ID#${CMAKE_C_COMPILER_ID}")
message("#COMPILER_CXX_HASH#${CXX_HASH}")
message("#COMPILER_CXX_VERSION#${CMAKE_CXX_COMPILER_VERSION}")
message("#COMPILER_CXX_ID#${CMAKE_CXX_COMPILER_ID}")
if(APPLE)
    message("#COMPILER_OBJC_HASH#${OBJC_HASH}")
    message("#COMPILER_OBJC_VERSION#${CMAKE_OBJC_COMPILER_VERSION}")
    message("#COMPILER_OBJC_ID#${CMAKE_OBJC_COMPILER_ID}")
    message("#COMPILER_OBJCXX_HASH#${OBJCXX_HASH}")
    message("#COMPILER_OBJCXX_VERSION#${CMAKE_OBJCXX_COMPILER_VERSION}")
    message("#COMPILER_OBJCXX_ID#${CMAKE_OBJCXX_COMPILER_ID}")
endif()

