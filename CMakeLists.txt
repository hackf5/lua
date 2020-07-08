cmake_minimum_required(VERSION 3.0.0)
project(
    lua 
    VERSION 5.4.0
    LANGUAGES C)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})

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

add_library(lua_core ${LUA_LIB_SRCS})
add_library(lua::lua ALIAS lua_core)

set_target_properties(lua_core PROPERTIES OUTPUT_NAME "lua")
target_include_directories(lua_core PUBLIC "include/lua")

set(LUA_DEFINITIONS)
if(UNIX)
    list(APPEND LUA_DEFINITIONS LUA_USE_POSIX)
endif()
target_compile_definitions(lua_core PUBLIC ${LUA_DEFINITIONS})
target_compile_options(lua_core PRIVATE "-Wall" "-Wextra")