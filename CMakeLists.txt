cmake_minimum_required(VERSION 3.0.0)
project(lua VERSION 5.4.0)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

# output paths
set(OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin/${CMAKE_BUILD_TYPE})
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${OUTPUT_DIRECTORY})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${OUTPUT_DIRECTORY})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${OUTPUT_DIRECTORY})

set(LUA_LIB_SRCS 
    "lapi.c"
    "lcode.c"
    "lctype.c"
    "ldebug.c"
    "ldo.c"
    "ldump.c"
    "lfunc.c"
    "lgc.c"
    "llex.c"
    "lmem.c"
    "lobject.c"
    "lopcodes.c"
    "lparser.c"
    "lstate.c"
    "lstring.c"
    "ltable.c"
    "ltm.c"
    "lundump.c"
    "lvm.c"
    "lzio.c"
    "lauxlib.c"
    "lbaselib.c"
    "lcorolib.c"
    "ldblib.c"
    "liolib.c"
    "lmathlib.c"
    "loadlib.c"
    "loslib.c"
    "lstrlib.c"
    "ltablib.c"
    "lutf8lib.c"
    "linit.c"
)

add_library(lua_static STATIC ${LUA_LIB_SRCS})
set_target_properties(lua_static PROPERTIES OUTPUT_NAME "lua")
set(LUA_DEFINITIONS)
if(UNIX)
    list(APPEND LUA_DEFINITIONS LUA_USE_POSIX)
endif()
target_compile_definitions(lua_static PUBLIC ${LUA_DEFINITIONS})
target_compile_options(lua_static PRIVATE "-Wall" "-Wextra")