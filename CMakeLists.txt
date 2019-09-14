CMAKE_MINIMUM_REQUIRED(VERSION 3.0.0)
PROJECT(unqlite)

# If the user did not customize the install prefix,
# set it to live under build so we don't inadvertently pollute /usr/local
IF(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  SET(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}/install" CACHE PATH "default install path" FORCE)
ENDIF(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_LIST_DIR}/src)

SET(HEADERS_UNQLITE
  unqlite.h
)

SET(SOURCES_UNQLITE
  src/os.c
  src/os_win.c
  src/os_unix.c
  src/mem_kv.c
  src/unqlite_vm.c
  src/bitvec.c
  src/pager.c
  src/jx9_vm.c
  src/jx9_vfs.c
  src/jx9_lib.c
  src/jx9_lex.c
  src/jx9_api.c
  src/jx9_json.c
  src/jx9_parse.c
  src/jx9_const.c
  src/jx9_memobj.c
  src/jx9_hashmap.c
  src/jx9_compile.c
  src/jx9_builtin.c
  src/api.c
)
#add_compile_definitions(UNQLITE_ENABLE_THREADS)
#add_compile_definitions(JX9_DISABLE_BUILTIN_FUNC)
#add_compile_definitions(JX9_DISABLE_DISK_IO)
SET(UNQLITE_STATIC_LIB unqlite)
ADD_LIBRARY(${UNQLITE_STATIC_LIB} STATIC ${HEADERS_UNQLITE} ${SOURCES_UNQLITE})
target_compile_definitions(${UNQLITE_STATIC_LIB} PRIVATE UNQLITE_ENABLE_THREADS JX9_DISABLE_BUILTIN_FUNC JX9_DISABLE_DISK_IO)
INSTALL(TARGETS ${UNQLITE_STATIC_LIB} COMPONENT devel ARCHIVE DESTINATION lib)
INSTALL(FILES ${HEADERS_UNQLITE} COMPONENT devel DESTINATION include)
