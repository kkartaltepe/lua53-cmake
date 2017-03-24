cmake_minimum_required(VERSION 3.4)

project(lua)

set(LUA_LIB_HEADER src/lualib.h src/lauxlib.h)
set(LUA_LIB_SRC src/lauxlib.c src/lbaselib.c src/lbitlib.c src/lcorolib.c src/ldblib.c
	src/liolib.c src/lmathlib.c src/loslib.c src/lstrlib.c src/ltablib.c src/lutf8lib.c
	src/loadlib.c src/linit.c)

set(LUA_CORE_HEADER src/lapi.h src/lcode.h src/lctype.h src/ldebug.h src/ldo.h src/lfunc.h
	src/lgc.h src/llex.h src/lmem.h src/lobject.h src/lopcodes.h src/lparser.h src/lstate.h
	src/lstring.h src/ltable.h src/ltm.h src/lundump.h src/lvm.h src/lzio.h)

set(LUA_CORE_SRC src/lapi.c src/lcode.c src/lctype.c src/ldebug.c src/ldo.c src/ldump.c
	src/lfunc.c src/lgc.c src/llex.c src/lmem.c src/lobject.c src/lopcodes.c
	src/lparser.c src/lstate.c src/lstring.c src/ltable.c src/ltm.c src/lundump.c
	src/lvm.c src/lzio.c)

set(LUA_BASE ${LUA_LIB_SRC} ${LUA_LIB_HEADER} ${LUA_CORE_SRC} ${LUA_CORE_HEADER})

add_definitions(-DLUA_BUILD_AS_DLL) # If building shared on windows
add_library(lua53 SHARED ${LUA_BASE})

add_executable(lua src/lua.c)
target_link_libraries(lua lua53)

set(LUA_C_SRC src/luac.c)
add_executable(luac ${LUA_C_SRC} ${LUA_CORE_HEADER} ${LUA_CORE_SRC})
target_link_libraries(luac lua53)
